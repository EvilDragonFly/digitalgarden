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

editable project
执行以下命令会执行当前目录的setup.py，将当前项目代码作为模块引入到环境的
对于无法联网的环境需要安装这个文件夹相关的module，可以先在外部环境pip install -e .当前目录生成egg-link文件。打包当前文件夹传到无法联网环境直接执行pip install -e .安装


```bash
pip install -e .

```

基于当前环境配置安装pip包

```bash
pip freeze > requirements.txt
conda create --name new_env requirements.txt

```

将指定目录创建conda环境

```bash
conda create --prefix= /usr/local/python3.7 python=3.7
conda activate /usr/local/python3.7

```

pip下载包到本地

```bash
pip download megatron==0.1 .

```
