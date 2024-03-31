---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/cpp/gcc/gcc attributes/","noteIcon":"3"}
---

https://stackoverflow.com/questions/11770451/what-is-the-meaning-of-attribute-packed-aligned4

### 1. alignment

```cpp

struct sSampleStruct1
{
     char Data1;
     //3-Bytes Added here.
     int Data2;
     unsigned short Data3;
     char Data4;
     //1-byte Added here.
}
sSampleStruct1

struct sSampleStruct2
{
     char Data1;
     int Data2;
     unsigned short Data3;
     char Data4;

}__attribute__((packed, aligned(1)))

sSampleStruct2

cout<<sizeof(sSampleStruct1)<<endl; // output: 12
cout<<sizeof(sSampleStruct2)<<endl; // output: 8

```



```cpp
printf("hello")

cout<< "world"

```


