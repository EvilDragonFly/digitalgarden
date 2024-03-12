---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/Build System/","noteIcon":"3"}
---

## cmake
cmake ..
cmake --build  .
cmake --install .
## make
```sh
make -j
make install -n     //  just print what files will install in where but does not install
make install
make target-name -j // make specific target
```

Makefile
- $< 表示源文件，这里指代SRC
- $@表示makefile中target name，这里也就是OBJ，目标文件
```sh
SRC = main.cpp
OBJ = main.o

all: $(OBJ)

$(OBJ): $(SRC)
    $(CXX) $(CXXFLAGS) $(CPPFLAGS) $< -o $@



```

基于megatron-lm 23.05学习python调用cpp
初步解释:
第一个target是default，前提依赖是也就是help.cpython-311-darwin.so，这里环境以macos举例
所有以.cpython-311-darwin.so后缀的target的依赖文件是当前目录下的所有cpp文件，生成这些so的方法是第9行指定的使用cpp编译器加上对应的flag，源文件就是%.cpp,输出结果就是指定的target，%$(LIBEXT):
```sh {9}
CXXFLAGS += -O3 -Wall -shared -std=c++11 -fPIC -fdiagnostics-color
CPPFLAGS += $(shell python3 -m pybind11 --includes)
LIBNAME = helpers
LIBEXT = $(shell python3-config --extension-suffix)

default: $(LIBNAME)$(LIBEXT)

%$(LIBEXT): %.cpp
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) $< -o $@

```