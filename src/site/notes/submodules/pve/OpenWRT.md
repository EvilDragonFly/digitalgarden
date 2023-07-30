---
{"dg-publish":true,"permalink":"/submodules/pve/OpenWRT/","noteIcon":""}
---

#network/openwrt #network/clash #network/proxy
# Deploy OpenWRT
## 1. upload openwrt img file to pve
you can upload from pve web or download can put to /var/lib/vz/template/iso/
## 2.create openwrt vm
![Pasted image 20230428130225.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428130225.png)

detach hard disk
![Pasted image 20230428130704.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428130704.png)

remove unused ide2 and disk
![Pasted image 20230428130931.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428130931.png)

execute command
```sh
qm importdisk 100 /var/lib/vz/template/iso/openwrt-22.03.4-x86-64-generic-ext4-combined-efi.img local-lvm
```
![Pasted image 20230428131243.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428131243.png)

set disk
![Pasted image 20230428131440.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428131440.png)

adjust boot order and make sata0 the first one to be booted
![Pasted image 20230428131644.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428131644.png)

## 3. add a linux bridge for openWRT
before we add bridge, network configuration is like this below:
![Pasted image 20230427235816.png](/img/user/submodules/pve/pics/Pasted%20image%2020230427235816.png)

after we add a network bridge on bond0
![Pasted image 20230428224131.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428224131.png)
start the openwrt vm and modify ip in /etc/config/network
![Pasted image 20230428224209.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428224209.png)

## 4. make openwrt use the bridge on bond0, so our laptop, ipad can be in the same network with openwrt.
proxmox web cannot detect what a bridge on a bond is
![Pasted image 20230428224416.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428224416.png)

Add we cannot edit the network device of openwrt in proxmox web to switch the base device from vmbr0 to br0.

![Pasted image 20230428224622.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428224622.png)


So we can only edit the opemwrt vm conf in pve shell
![Pasted image 20230428224754.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428224754.png)

## 6. login openwrt
![Pasted image 20230428224925.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428224925.png)


# Deploy Clash in OpenWRT
## 1. config dns and region

![Pasted image 20230428231323.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428231323.png)

![Pasted image 20230428232919.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428232919.png)

![Pasted image 20230428232548.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428232548.png)

![Pasted image 20230428232951.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428232951.png)

apply the change
![Pasted image 20230428231603.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428231603.png)

check change in openwrt shell

![Pasted image 20230428232852.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428232852.png)

now we can ping baidu.com in the openwrt shell

![Pasted image 20230429003130.png](/img/user/submodules/pve/pics/Pasted%20image%2020230429003130.png)

## 1. download clash

![open clash for openwrt](https://github.com/vernesong/OpenClash)

after install openclash, reboot
add clash subcription
![Pasted image 20230429013630.png](/img/user/submodules/pve/pics/Pasted%20image%2020230429013630.png)


## 2.config end device
config the client device network: make sure gateway and dns is the ip of openWRT
![c5837995c81f57ff3a0441748641eb2.jpg](/img/user/submodules/pve/pics/c5837995c81f57ff3a0441748641eb2.jpg)


## 3. some additional settings
### 3.1 visit bing.com instead of cn.bing.com
As I wanna use new bing's chat AI in clash rule mode(it work in clash global mode), I need to overwrite clash default rule mode to make bing.com does not go to cn.bing.com.
go to openclash and download clash rule file
![Pasted image 20230711215316.png](/img/user/submodules/pve/pics/Pasted%20image%2020230711215316.png)

we can see all the aviable proxy node
![Pasted image 20230711215607.png](/img/user/submodules/pve/pics/Pasted%20image%2020230711215607.png)

use one node which area bing is not blocked
![Pasted image 20230711215746.png](/img/user/submodules/pve/pics/Pasted%20image%2020230711215746.png)
click apply setting.
now go into clash yacd web and check if the new rule is working
![Pasted image 20230711215915.png](/img/user/submodules/pve/pics/Pasted%20image%2020230711215915.png)


now I can use bing's chat AI
![Pasted image 20230711220000.png](/img/user/submodules/pve/pics/Pasted%20image%2020230711220000.png)
