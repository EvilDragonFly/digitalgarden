---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/disk/from disk to lvm/","noteIcon":"3"}
---

#disk #lvm
### 1.逻辑卷创建
![Pasted image 20240205110736.png|undefined](/img/user/Pasted%20image%2020240205110736.png)

### 2.逻辑卷挂载
![Pasted image 20240205111337.png|undefined](/img/user/Pasted%20image%2020240205111337.png)
/etc/fstab文件加入挂载lvm卷
```bash
/dev/mapper/vgruntime-lvruntime /runtime ext4 default 0 2

```
