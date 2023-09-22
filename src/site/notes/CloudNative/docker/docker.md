---
{"dg-publish":true,"permalink":"/CloudNative/docker/docker/","noteIcon":"","created":"","updated":""}
---

#docker
## 1. docker的代理
docker和maven，npm类似，代理和系统代理不一样需要单独配置，具体配置参考[docker docs](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy)
关于docker的配置代理的文件主要是两个，可以根据需要编辑其中一个或者两个一起
/etc/docker/daemon.json
![Pasted image 20230922224955.png](/img/user/Pasted%20image%2020230922224955.png)
/etc/systemd/system/docker.service.d/http-proxy.conf

![Pasted image 20230922225041.png](/img/user/Pasted%20image%2020230922225041.png)
编辑添加代理之后可以通过以下命令生效并查看是否成功生效

```bash
systemctl daemon-reload
systemctl restart docker
systemctl show --property=Environment docker
```

## 2. Dockerfile的编写
```bash
ARG base=debian:v0  # 指定基础镜像，给出默认值，可以从docker build指定值覆盖
FROM $bash
ARG arg1 # 声明参数, 注意docker build指定的build arg最好得在dockerfile中声明
ARG arg2 # 声明参数
USER root
CP *.deb /home
RUN command1 $arg1 && \
command2 $arg2
```
在Dockerfile所在的路径执行

```bash
docker build -t . --build-arg arg1='a' --build-arg='b'

```
## 3. Docker的镜像
docker镜像可以直接由dockerfile制备，或者可以将运行中的容器当前的文件系统和状态保存下来

```bash
docker commit container_name repo:tag #将当前容器状态保存到镜像repo:tag
docker save repo:tag > repo.tar # 将镜像保存到本地文件repo.tar
docker load < repo.tar # 从本地文件导入镜像

```

export/import与save/load的区别
> export是从容器导出，save是从镜像导出，save会保存所有layer的信息，export不会保存所有layer的信息，因此导出文件更小，但是没法回滚


## 4.容器的进出

退出当前container而不stop当前container(exit会stop容器)

```bash
ctrl p q
```


进入到容器
```bash
docker exec -it container_name bash
docker attach container_name 
```
> [具体来说，`docker exec`命令会在容器内部启动一个新的进程，以执行指定的命令](https://www.zhihu.com/question/276485274)[1](https://www.zhihu.com/question/276485274). [而`docker attach`命令则会将标准输入和输出连接到容器内部的PID 1，实现对容器内正在执行的终端的附着](https://www.zhihu.com/question/276485274)[1](https://www.zhihu.com/question/276485274)

## 5. 容器文件互传

```bash
docker cp container_name:path host_path
docker cp host_path container_name:path
```