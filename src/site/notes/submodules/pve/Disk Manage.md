---
{"dg-publish":true,"permalink":"/submodules/pve/Disk Manage/","noteIcon":""}
---

#disk
I give a small size to proxmox when a install it, which make the local-lvm size not enough to create many vm and store iso. So I need to extend the local-lvm to the full size of my os disk.
## 1. Extend the partition
before my operation, the partition and lvm is like below:
![Pasted image 20230424235158.png](/img/user/submodules/pve/pics/Pasted%20image%2020230424235158.png)

```sh
fdisk /dev/sda    ## make sure the disk is the last partition of the disk
>> p              ## rember the fist sector number
>> d
>> 3
>> n              ## make sure the first sector number is the same before
>> p              ## primary partition
>> w
```
now lsblk output will show that /dev/sda3 is 930.5G, but still we need to extend the pve-data logical volume
## 2.Resize the physical volume
use pvdisplay, the result show that the pv /dev/sda3 is still not change(200G).
![Pasted image 20230425000225.png](/img/user/submodules/pve/pics/Pasted%20image%2020230425000225.png)
```sh
pvresize /dev/sda3
```
after resize the pg, the vg is also back to normal
![Pasted image 20230425000328.png](/img/user/submodules/pve/pics/Pasted%20image%2020230425000328.png)

## 3.extend the logical volume
With the vg having enough space, we can extend the local-lvm
![Pasted image 20230425001038.png](/img/user/submodules/pve/pics/Pasted%20image%2020230425001038.png)

```sh
lvextend -r -l +100%FREE /dev/pve/data
```

## Related posts
[resize partition](https://www.ibm.com/docs/en/cloud-pak-system-w3550/2.3.3?topic=images-extending-partition-file-system-sizes)

[lv, vg and pv](https://networklessons.com/uncategorized/extend-lvm-partition)

[resize lv](https://unix.stackexchange.com/questions/138090/cant-resize-a-partition-using-resize2fs)