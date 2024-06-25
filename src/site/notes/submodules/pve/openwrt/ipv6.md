---
{"dg-publish":true,"permalink":"/submodules/pve/openwrt/ipv6/","noteIcon":"3"}
---

#ipv6 #adb

https://www.right.com.cn/forum/thread-8320635-1-1.html
禁止科学上网

### 1. 设置op ipv6网关
```sh
# 1 登录 ssh
        sendat 2 'AT+QADBKEY?' #(获取密钥
        #浏览器打开 https://onecompiler.com/python/3znepjcsq 把第一部获取的密钥粘贴进去点击 RUN 将得到 key
        sendat 2 'AT+QADBKEY="获取的key"' #(写入key
        sendat 2 'AT+QCFG="usbcfg",0x2C7C,0x0801,1,1,1,1,1,1,0' #(开启 ADB
        sendat 2 'AT+CFUN=1,1' #(重启模块
# 2 安装ADB

        opkg update && opkg install adb
        adb devices #(查看 ADB 是否开启成功)
        #List of devices attached 6af80141 device（出现类似内容既开启成功

#3 添加开机脚本
        vim /etc/hotplug.d/iface/90-ipv6gwadd
        # 写入如下内容
        #!/bin/sh
        [ "$ACTION" = ifup ] || exit 0
        [ "$INTERFACE" = wan ] || exit 0
        sleep 15s
        ipv6_gateway="$(ip -6 route show default | awk '/default/ {print $3}')"
        adb shell ip -6 route add $ipv6_gateway dev bridge0 metric 100 pref medium
        ip -6 route add $ipv6_gateway dev br-lan

#4 重启 660
ip -6 route
```
![Pasted image 20240407161517.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240407161517.png)

### 2. wan
DHCP client
![Pasted image 20240407160912.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240407160912.png)

![Pasted image 20240407161000.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240407161000.png)
### 3. wan6
DHCPv6 client
![Pasted image 20240407160733.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240407160733.png)

![Pasted image 20240407161018.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240407161018.png)
### 4. lan

![Pasted image 20240407161124.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240407161124.png)


### 5. 设置openclash ipv6 dns解析


![Pasted image 20240424123408.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240424123408.png)




wired connection


https://forum.proxmox.com/threads/how-to-setup-proxmox-for-ipv6-in-my-homenet.135475/post-599624
https://www.saudiqbal.com/blog/ipv6-home-server-with-dynamic-prefix-for-vpn-web-server-rdp-and-firewall-setup-guide.php


设置网线直连的proxmox网卡获取到公网ipv6


https://wiki.debian.org/IPv6PrefixDelegation
https://openwrt.org/docs/guide-user/network/ipv6/configuration

https://sysctl-explorer.net/net/ipv6/accept_ra/

![Pasted image 20240412192126.png](/img/user/submodules/pve/openwrt/attachments/Pasted%20image%2020240412192126.png)




