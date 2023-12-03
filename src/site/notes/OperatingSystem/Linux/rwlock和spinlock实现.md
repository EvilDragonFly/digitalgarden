---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/rwlock和spinlock实现/","noteIcon":"3"}
---

一下源码分析基于linux 6.6.1
sparce
https://lwn.net/Articles/689907/

```cpp
#define acquire __context__(x,1)

```

https://hackmd.io/@sysprog/linux-sync
https://gcc.gnu.org/bugzilla/show_bug.cgi?id=59856
https://lwn.net/Articles/689907/
https://lwn.net/Articles/109066/
https://sparse.docs.kernel.org/_/downloads/en/doc-ptrlist/pdf/

## rwlock

\_\_raw_read_lock
include/linux/rwlock_api_smp.h

```cpp
static inline void __raw_read_lock(rwlock_t *lock)

{

preempt_disable();

rwlock_acquire_read(&lock->dep_map, 0, 0, _RET_IP_);

LOCK_CONTENDED(lock, do_raw_read_trylock, do_raw_read_lock);

}

```

include/linux/rwlock.h
```cpp
# define do_raw_read_lock(rwlock) do {__acquire(lock); arch_read_lock(&(rwlock)->raw_lock); } while (0)

```

include/linux/compiler_types.h
这里的\_\_context\_\_还有\_\_attribute\_\_((context(x,1,1)))为sparse实现，主要功能是操作context的引用计数
```cpp
/* context/locking */

# define __must_hold(x) __attribute__((context(x,1,1)))

# define __acquires(x) __attribute__((context(x,0,1)))

# define __cond_acquires(x) __attribute__((context(x,0,-1)))

# define __releases(x) __attribute__((context(x,1,0)))

# define __acquire(x) __context__(x,1)

# define __release(x) __context__(x,-1)

# define __cond_lock(x,c) ((c) ? ({ __acquire(x); 1; }) : 0)

```


include/linux/rwlock_types.h
```cpp
typedef struct {

arch_rwlock_t raw_lock;

#ifdef CONFIG_DEBUG_SPINLOCK

unsigned int magic, owner_cpu;

void *owner;

#endif

#ifdef CONFIG_DEBUG_LOCK_ALLOC

struct lockdep_map dep_map;

#endif

} rwlock_t;

```

## spinlock
arch/arm/include/asm/spinlock_types.h
```cpp
typedef struct {

union {

u32 slock;

struct __raw_tickets {

#ifdef __ARMEB__

u16 next;

u16 owner;

#else

u16 owner;

u16 next;

#endif

} tickets;

};

} arch_spinlock_t;

```

arch/arm/include/asm/spinlock.h
```cpp
static inline void arch_spin_lock(arch_spinlock_t *lock)

{
unsigned long tmp;
u32 newval;
arch_spinlock_t lockval; 
prefetchw(&lock->slock);
__asm__ __volatile__(

"1: ldrex %0, [%3]\n"

" add %1, %0, %4\n"

" strex %2, %1, [%3]\n"

" teq %2, #0\n"

" bne 1b"

: "=&r" (lockval), "=&r" (newval), "=&r" (tmp)

: "r" (&lock->slock), "I" (1 << TICKET_SHIFT)

: "cc");

  

while (lockval.tickets.next != lockval.tickets.owner) {

wfe();

lockval.tickets.owner = READ_ONCE(lock->tickets.owner);

}

  

smp_mb();

}

```
以上汇编代码简化成cpp功能如下

```cpp
static inline void arch_spin_lock(arch_spinlock_t *lock) {
    arch_spinlock_t local_lock;
 
    local_lock.slock = lock->slock; /* 1 */
    lock->tickets.next++; /* 2 */ //系统下一个取号码+1
    // 当发现系统当前可办理业务的编号和自己取的号码一致的时候可以直接办理业务，否则等待，不时抬头检查
    while (local_lock.tickets.next != local_lock.tickets.owner) { /* 3 */
        wfe(); /* 4 */
        local_lock.tickets.owner = lock->tickets.owner; /* 5 */ // 抬头更新记录一下系统最新的办理人编号
    }
} 
```
