---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/python/pip/","noteIcon":"","created":"","updated":""}
---

#python/pip
pip常用命令

```bash
pip show rich # 显示当前已安装包的信息
pip install rich==13.5.2 -i http://... --trusted-host mirrors.huaweicloud.com
pip config list
pip config set global.proxy ....
pip uninstall rich # 卸载包的缓存文件在~/.cache/pip中，之后重新install会从缓存中获取
pip cache purge # 清除所有缓存文件
```