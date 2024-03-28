---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/python/built-in functions/","noteIcon":"3"}
---

https://www.pythontutorial.net/python-oop/python-__repr__/

`__str__` and `__repr__`


|          | `__str__`                                                                                                                                                          | `__repr__`                                                                                                                                                                                                                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 含义       | returns a string representation of an object <br>that is human-readable,<br>通常如果未自定义实现,会调用`__repr__`<br>`str()`最后调用此方法，通常`print(a)`会调用`str()`,最后调用到a的`__str__`     | returns a string representation of an object that is machine-readable<br>Typically, the `__repr__()` returns a string that can be executed and yield the same value as the object.<br>In other words, if you pass the returned string of the `object_name.__repr__()` method to the `eval()` function, you’ll get the same value as the `object_name` |
| examples | ```py<br>from dataclasses import dataclass<br>@dataclass<br>class Point:<br>   x: int<br>   y: int<br>a = Point(10,20)<br># usins str()<br>print(a)<br><br><br>``` | ```py<br>from dataclasses import dataclass<br>@dataclass<br>class Point:<br>   x: int<br>   y: int<br>a = Point(10,20)<br>print(repr(a))<br>```                                                                                                                                                                                                       |
|          |                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                       |


```py

class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age

    def __repr__(self):
        return f'Person("{self.first_name}","{self.last_name}",{self.age})'

person = Person("John", "Doe", 25)
print(repr(person))

```