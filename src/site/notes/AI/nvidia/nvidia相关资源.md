---
{"dg-publish":true,"permalink":"/AI/nvidia/nvidia相关资源/","noteIcon":"3"}
---

#nvidia #docker
https://blog.csdn.net/seasermy/article/details/105298646

[nvidia申请账号密钥密码](https://ngc.nvidia.com/setup/api-key)

[nvidia相关镜像tag](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch/tags)



```sh

docker login nvcr.io
Username: $oauthtoken
Password: Z2k3YWdzbmpydDhiZ205Mjdkcm1xZjFmYjoxYTI1NzAxMy01YzA0LTRmNTctYjk4Zi1iMTE3N2MxOTQ1Mjk
```


nvidia docker container setup

```sh
docker run -it  --gpus all --net host --name xxl-dahua1 \
--shm-size=64G \
-v /data:/data \
nvcr.io/nvidia/pytorch:23.04-py3 /bin/bash
```