---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/cpp/algorithm/build-in algorithm/","noteIcon":"3"}
---

### 1. all_of, any_of, none_of

第三个参数是`unary predicate`
```cpp
// if all elements is '0', then result is "0"
#include<vector>

auto a = vector<int>(5,0)
all_of(a.cbegin(), a.cend(), [](int e) { return e == 0; })

auto b = vector<int>{0,0,1,0}
any_of(b.cbegin(), b.cend(), [](int e) { return e == 1; })

none_of(a.cbegin(), a.cend(), [](int e) { return e != 0; })

```