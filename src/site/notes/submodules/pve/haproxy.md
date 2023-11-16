---
{"dg-publish":true,"permalink":"/submodules/pve/haproxy/","noteIcon":"3"}
---


#proxy #reverseproxy #haproxy
haproxy配置参考

```bash
# Example configuration file for HAProxy 2.0, refer to the url below for
# a full documentation and examples for configuration:
# https://cbonte.github.io/haproxy-dconv/2.0/configuration.html


# Global parameters
global

	# Log events to a remote syslog server at given address using the
	# specified facility and verbosity level. Multiple log options 
	# are allowed.
	#log 10.0.0.1 daemon info

	# Specifiy the maximum number of allowed connections.
	maxconn 32000

	# Raise the ulimit for the maximum allowed number of open socket
	# descriptors per process. This is usually at least twice the
	# number of allowed connections (maxconn * 2 + nb_servers + 1) .
	ulimit-n 65535

	# Drop privileges (setuid, setgid), default is "root" on OpenWrt.
	uid 0
	gid 0

	# Perform chroot into the specified directory.
	#chroot /var/run/haproxy/

	# Daemonize on startup
	daemon

	nosplice
	# Enable debugging
	#debug

	# Spawn given number of processes and distribute load among them,
	# used for multi-core environments or to circumvent per-process
	# limits like number of open file descriptors. Default is 1.
	#nbproc 2

# Default parameters
defaults
	# Default timeouts
	timeout connect 5000ms
	timeout client 50000ms
	timeout server 50000ms
	timeout http-keep-alive 10s
	maxconn 30

# Special health check listener for integration with external load
# balancers.
listen local_health_check

	# Listen on port 60000
	bind :60000

	# This is a health check
	#mode health
	http-request return status 200
	

	# Enable HTTP-style responses: "HTTP/1.0 200 OK"
	# else just print "OK".
	option httpchk

listen admin_stats
	stats enable
	bind :1188
	mode http
	option httplog
	log global
	maxconn 10
	stats refresh 5s
	stats uri /admin
	stats realm haproxy
	stats auth admin:admin
	stats admin if TRUE



frontend containers
	bind :81 transparent
	timeout client 30s
	mode http
	acl calibre  hdr(host) -i calibre.lan
	acl mediacms hdr(host) -i mediacms.lan
	use_backend calibre if calibre
	use_backend mediacms if mediacms
	default_backend mediacms

backend calibre
	mode http
	option httpchk
	timeout connect 5000
	timeout server 30s
	server s1 192.168.66.11:8083 weight 1 rise 2 fall 3
backend mediacms
	mode http
	option httpchk
	timeout connect 5000
	timeout server 3s
	server s1 192.168.66.11:80 weight 1 rise 2 fall 3


```

haproxy配置完reload之后可以使用自带的命令进行检测配置是否valid
`service haproxy check`

![Pasted image 20231116000811.png|undefined](/img/user/submodules/pve/pics/Pasted%20image%2020231116000811.png)

成功访问haproxy统计页面
![Pasted image 20231116004421.png|undefined](/img/user/submodules/pve/pics/Pasted%20image%2020231116004421.png)