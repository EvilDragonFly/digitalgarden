---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/shell/shell脚本的一些tricks/","noteIcon":"3"}
---

#shell
### 1. 字符串内替换

```bash
os="Mac OS X"
# 语法: ${variable//pattern/replacement}
echo ${os// /}
```

### 2. 文件拆分和压缩
#split

```bash
#默认aa,ab这种后置
split -l 100 large_file.log part_
#以400行作为一个part拆分，使用数字后缀，前缀指定为part_,并显示分割进度
split -l 400 -d large_file.log part_ --verbose
#按文件大小拆分
split -b 1G large_file.log part_
#拆分数据还原
cat part_* > merge_file.log
#压缩文件
tar -zcvf large_file.tar.gz large_file
#解压
tar -zxvf latrge_file.tar.gz
zip -r large.zip large
# 压缩的文件比较大的话可以使用pv显示进度,这里-表示stdout or stdin，取决于命令中的位置，需要明确的是这不是shell内置的而是取决于具体命令的实现
tar cf - $path | pv -s $(du -sb $path|awk '{print $1}') | gzip > file.tar.gz

```

#file
### 3.查找文件
#find #file
[参考](https://www.myfreax.com/find-large-files-in-linux/)

```shell
# 查找大文件
find . -xdev -type f -size +100M -print | xargs ls -lh | \
sort -k5,5 -h -r | head
# 查看文件夹内文件个数
find . -type f |wc -l
tree | tail -1
```

### 4. 使用alias
#alias #shopt

```bash
#一些软件安装是直接拉取指定链接文件直接本地执行，这些脚本文件中可能会使用wget和curl来拉取依赖
#这些工具可能会存在ssl认证的问题，为了能顺利执行，我们可以将脚本拉取到本地，在脚本内第一行使用alias
# 第一行务必使用shopt开启alias展开。。
shopt -s expand_aliases
alias curl='curl -k'
alias wget='wget --no-check-certificate'

```

### 6. 常见函数



8. 