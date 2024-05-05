---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/cpp/cpp-concurrency/mutex/","noteIcon":"3"}
---

### summaries

1.针对mutex的lock和unlock操作，为了防止出现exception或者其他分支情况导致锁未释放，推荐使用具有RAII思想的`std::lock_guard`

```cpp
#include <list>
#include <mutex>
#include <algorithm>
std::list<int> some_list;
std::mutex some_mutex;
void add_to_list(int new_value)
{
std::lock_guard<std::mutex> guard(some_mutex);
some_list.push_back(new_value);
}
bool list_contains(int value_to_find)
{
std::lock_guard<std::mutex> guard(some_mutex);
return std::find(some_list.begin(),some_list.end(),value_to_find)
!= some_list.end();
}

```



2.对于protected data，mutex可以在cpp文件中当做global variable，一些针对protected data的操作需要获取mutex，但是有限推荐使用面向对象的思想将protected data，mutex lock还有对应的operations封装到一个类中，针对protected data的操作为类中的私有函数
3.对于类中被mutex保护的protected data，如果存在一个member function能返回对应数据的reference or pointer，所有的lock都是徒劳，因为这会给对应的protected data留下一个backhole，其他threads即使没有获取到lock但是通过reference or pointer都可以modify protected data