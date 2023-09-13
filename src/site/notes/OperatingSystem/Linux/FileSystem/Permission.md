---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/FileSystem/Permission/","noteIcon":"","created":"","updated":""}
---

1. 一般linux的默认umask为022，创建的文件默认没有执行权限
如下图，创建的folder的权限为777-022=755，创建的file的权限为666-022=644
![Pasted image 20230913224224.png](/img/user/pics/Pasted%20image%2020230913224224.png)
3. 脚本测试对应路径的的属组和其他属组是否存在写权限
#stat #cut

```bash
if [ "$(stat -c '%A' "${path}|cut -c6")" == w ]; then
	echo "${path} does not comply with security rules groups write. exiting"
	return 1
fi
if [ "$(stat -c '%A' "${path}|cut -c9")" == w ]; then
	echo "${path} does not comply with security rules other write. exiting"
	return 1
fi

```

