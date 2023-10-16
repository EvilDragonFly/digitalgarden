---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/shell/shell脚本的一些tricks/","noteIcon":"","created":"","updated":""}
---

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

3. 