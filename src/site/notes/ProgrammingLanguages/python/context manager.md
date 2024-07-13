---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/python/context manager/","noteIcon":"3"}
---


https://stackoverflow.com/questions/1984325/explaining-pythons-enter-and-exit

> [!NOTE] With statement
> **with** statement only works with objects that support the context management protocol (i.e. they have `__enter__` and `__exit__` methods). A class which implement both methods is known as context manager class.

with语句可以支持context manager的类，也就是实现了`__enter__`和`__exit__`的类，通过在with block的开始的时候会调用`__enter__`方法来申请资源，在with block结束的时候调用`__exit__`来进行释放资源