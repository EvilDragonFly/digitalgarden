---
{"dg-publish":true,"permalink":"/ProgrammingLanguages/python/pip/","noteIcon":"3"}
---

#python/pip #pip
![freestocks-flOVXZWbjJ4-unsplash.jpg|100%](/img/user/banner/freestocks-flOVXZWbjJ4-unsplash.jpg)
### pip常用命令
pip配置文件:~/.pip/pip.config，配置示例，pip使用系统代理就行

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
extra-index-url=
    https://pypi.mirrors.ustc.edu.cn/simple/
    https://pypi.douban.com/simple/
    https://pypi.python.org/simple/
[install]
trusted-host = tuna.tsinghua.edu.cn
    pypi.douban.com
    mirrors.ustc.edu.cn
    python.org


```



```bash
pip show rich # 显示当前已安装包的信息
pip install rich==13.5.2 -i http://... --trusted-host mirrors.huaweicloud.com
# 查看config
pip config list
pip -v config list # 可查看到具体加载的那些配置文件和内容
pip config set global.proxy ....
pip uninstall rich # 卸载包的缓存文件在~/.cache/pip中，之后重新install会从缓存中获取
pip cache purge # 清除所有缓存文件

pip install --no-index --find-links=deps --no-build-isolation psycopg[c]
# 查看pip包有什么版本
pip install datasets==
#设置超时时间
pip install datasets --default-time=200
#安装包，不使用cache文件
pip install torch --no-cache-dir

#保存当前环境配置
pip freeze > requirements.txt
# 下载指定包到本地
pip download -r requirements.txt --dest . --no-deps
```

editable project
执行以下命令会执行当前目录的setup.py，将当前项目代码作为模块引入到环境的
对于无法联网的环境需要安装这个文件夹相关的module，可以先在外部环境pip install -e .当前目录生成egg-link文件。打包当前文件夹传到无法联网环境直接执行pip install -e .安装


```bash
pip install -e .
# or
python setup.py install

```

![Pasted image 20231028220804.png|80%](/img/user/pics/Pasted%20image%2020231028220804.png)
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
pip download megatron==0.1 --no-deps
# pip默认会下载当前pip对应的本地python版本的whl包，我们可以指定别的python版本
pip download megatron==0.1 --python-version 3.9 --no-deps

```

### conda复用环境
#### 在线安装方式
**创建一个新的Python 3.8环境：** 首先，在Conda中创建一个新的Python 3.8环境。你可以使用以下命令来创建一个名为`py38env`的环境：

- `conda create --name py38env python=3.8`
    
- **激活新环境：** 激活新创建的Python 3.8环境：
    
- `conda activate py38env`
- **复制包列表：** 现在，你需要从Python 3.7环境中导出已安装包的列表。可以使用以下命令导出包列表：
- `conda list --export > package_list.txt`

- **安装包到新环境：** 使用以下命令，将导出的包列表安装到新的Python 3.8环境中：   

`conda install --name py38env --file package_list.txt`

这将安装与Python 3.7环境相同的包到新的Python 3.8环境中，可能存在部分包不支持3.8，需要手动升级了
#### 离线拷贝方式

克隆已有环境
```bash
conda create -n env2 python=3.9 --clone env1
```
**通过硬链接复制已安装的包：**

1. 首先，在Python 3.8环境中创建一个新的虚拟环境（如果尚未创建），并激活它：
- `conda create --name py38env python=3.8 
   `conda activate py38env` 
- 找到Python 3.7环境中的`site-packages`目录，这是已安装包的位置。你可以使用以下命令查找它：
- `conda list --name py37env`
    查找输出中的 `site-packages` 目录。
- 切换到Python 3.8环境，然后创建硬链接以复制Python 3.7环境中的包到Python 3.8环境。假设你找到的`site-packages`目录是 `/path/to/py37env/lib/python3.7/site-packages`，可以使用以下命令：
	`ln -s /path/to/py37env/lib/python3.7/site-packages/* /path/to/py38env/lib/python3.8/site-packages/` 
- 这会在Python 3.8环境中创建硬链接到Python 3.7环境中的包。 
- 验证已经复制了包，你可以运行以下命令检查：

 `conda list --name py38env` 
这将显示已经安装的包列表。
这种方法可以帮助你在不重新下载包的情况下复用Python 3.7环境中的包到Python 3.8环境中。然而，要注意的是硬链接可能会在不同的环境之间引入一些潜在问题，因此在执行此操作之前请谨慎考虑。确保你理解这种方法可能带来的潜在风险。