---
{"dg-publish":true,"permalink":"/submodules/pve/Network Manage/","noteIcon":""}
---

After pve set up, we should some network configuration for vms to make they can connect with each other and outside network.

## domain resolve
After the zerotier is set up, we can set a hostname for proxmox server's zerotier ip to coveniently connect to proxmox web in browser.
![Pasted image 20230425235839.png](/img/user/submodules/pve/pics/Pasted%20image%2020230425235839.png)

![Pasted image 20230425235934.png](/img/user/submodules/pve/pics/Pasted%20image%2020230425235934.png)
## vms' bridge
make sure that vmbr0 is after the wlp4s0.
### bad example1:bridge enslave ethernet card and wireless card
![Pasted image 20230426210338.png](/img/user/submodules/pve/pics/Pasted%20image%2020230426210338.png)

![Pasted image 20230426210301.png](/img/user/submodules/pve/pics/Pasted%20image%2020230426210301.png)

when we reboot the pve, we cannot have ip in enp3s0 and wlp4s0, and if we set up one og them, it will print the error **ignoring ip address assigning an ip  address is not allowed on enslaved interface**

###  bad example2: ethernet card and wireless card in the same network without a bond.
![Pasted image 20230426233411.png](/img/user/submodules/pve/pics/Pasted%20image%2020230426233411.png)

Though we does not enslave interfaces in vmbr0, but only enp3s0 can work, because both interfaces in the same network is confusing the routing. Result is that we cannot connect to network with wlp4s0(only enp3s0 works), which make vms that base the nat does not connect to network as well.
[why we cannot connect to network using wireless card when ethernet and wireless card connect to the same LAN](https://unix.stackexchange.com/questions/153060/wireless-interface-only-reachable-when-ethernet-cable-plugged-in)

## Good Example: build a bond
apt install ifenslave
[create a bond in debian](https://wiki.debian.org/Bonding)
make sure wpa-bridge is after wpa-conf

![Pasted image 20230427235816.png](/img/user/submodules/pve/pics/Pasted%20image%2020230427235816.png)

![Pasted image 20230428001533.png](/img/user/submodules/pve/pics/Pasted%20image%2020230428001533.png)

## vm network configuration example
Here is an network configuration of ubuntu2204.
![Pasted image 20230425233452.png](/img/user/submodules/pve/pics/Pasted%20image%2020230425233452.png)