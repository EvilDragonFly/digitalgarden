---
{"dg-publish":true,"permalink":"/submodules/pve/openclash bypass原理/","noteIcon":"3"}
---

![Pasted image 20231120021753.png|100%](/img/user/Pasted%20image%2020231120021753.png)
专门下载wireshark在客户端mac抓包，路由openwrt服务器上tcpdump抓包，但是有用的信息只有mac与openwrt之间9090端口通信，也就是openclash内监听的端口之一，但是为啥mac会与openclash的9090端口进行通信(mac上运行clashx是直接在设置里制定了代理为本地的对应端口)还有openclash直接格端口之间的内部是否有转发什么之类的无从得知。
首先查看dnsmasq的配置发现并没有什么openclash添加的文件，之前安装haproxy想实现配置域名端口解析在firewall配置文件中发现了openclash的一些配置

![Pasted image 20231120021058.png|undefined](/img/user/Pasted%20image%2020231120021058.png)

![Pasted image 20231120021142.png|undefined](/img/user/Pasted%20image%2020231120021142.png)

想要探查openclash的实现，不得不去查阅openclash基于的内核clash，但是clash已经被owner给删库了，但是还好https://archive.org/有hero上传备份