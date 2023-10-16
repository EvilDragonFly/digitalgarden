---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/packages/rpm/","noteIcon":"","created":"","updated":""}
---

#rpm #yum

设置yum安装包时不进行ssl校验

#ssl
```bash
# 编辑/etc/yum.conf,在[main]下加上
sslverify=false

```


查看rpm包,例如test安装的文件

```bash
rpm -qa|grep test
rpm -ql test
```

查看rpm包的信息
`rpm -qi test`

yum 更新

```bash
yum clean all
yum makecache
```

查看安装包在那个repo中包含
```bash
repoquery -i gazelle
```

glibc降级
```bash
yum downgrade glibc\* --allowerasing
```
查看文件对应的rpm包
`rpm -qf filepath`

下载rpm到本地

```bash
yum install libtirpc-gen --downloadonly --destdir .
#使用yum-utils中的命令
yumdownloader package_name

```


