---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/cpp/cpp-concurrency/dead lock/","noteIcon":"3"}
---

#deadlock
对于死锁问题可以用一个toy来进行举例，一个toy包含两个组件drum and drumstick，两个小孩想要击鼓的话需要同事持有drum and drumstick才能正常跑起来，但是如果A拿到了drum，B拿到了drumstick，除非其中一个be nice and give the other piece, 否则就会出现两个小孩都没法玩，在concurrency场景下的deadalock问题
避免死锁问题的一般解决方法
### 1. lock mutex in the same order
每个进程必须先hold mutex A then hold mutex B，然而如果A和B是protect同一个类的不同instances的话就没法区分
### 2. lock multiple mutex in one call provided by C++ Standard Library
C++ 标准库实现lock可以同时持有多个mutex，并且防止出现deadlock
deadlock avoidance algorithm to avoid deadlock.
```cpp
class some_big_object;
void swap(some_big_object& lhs, some_big_object& rhs);
class X {
 private:
  some_big_object some_detail;
  std::mutex m;

 public:
  X(some_big_object const& sd) : some_detail(sd) {}
  friend void swap(X& lhs, X& rhs) {
    if (&lhs == &rhs) return;
    std::lock(lhs.m, rhs.m);
    // adopt_lock used to assume the calling thread already has ownership of the mutex without having to relock
    // using lock_guard to make sure both already-locked mutexes are unlocked at the end of scope
    std::lock_guard<std::mutex> lock_a(lhs.m, std::adopt_lock);
    std::lock_guard<std::mutex> lock_b(rhs.m, std::adopt_lock);
    swap(lhs.some_detail, rhs.some_detail);
  }
};
```