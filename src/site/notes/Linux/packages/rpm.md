---
{"dg-publish":true,"permalink":"/Linux/packages/rpm/","dgPassFrontmatter":true,"noteIcon":""}
---

#rpm #yum
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

