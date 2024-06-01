```
# /var/lib/lxc/dnsx
# Template used to create this container: /usr/share/lxc/templates/lxc-debian+  
# Parameters passed to the template: -r bookworm --packages=nano,iputils-ping  
# For additional config options, please look at lxc.container.conf(5)  
  
# Uncomment the following line to support nesting containers:  
#lxc.include = /usr/share/lxc/config/nesting.conf  
# (Be aware this has security implications)  
  
lxc.start.auto = 0  
lxc.start.order = 10  
  
lxc.net.0.type = veth  
lxc.net.0.hwaddr = 00:16:3e:01:3b:0a  
lxc.net.0.link = br0  
lxc.net.0.flags = up  
lxc.net.0.ipv4.address = 10.7.3.10/16  
lxc.net.0.ipv4.gateway = 10.7.3.1  
lxc.net.0.veth.pair = veth10  
  
lxc.apparmor.profile = generated  
lxc.apparmor.allow_nesting = 1  
lxc.rootfs.path = dir:/var/lib/lxc/dns3/rootfs  
  
# Common configuration  
lxc.include = /usr/share/lxc/config/debian.common.conf  
  
# Container specific configuration  
lxc.tty.max = 4  
lxc.uts.name = dns3  
lxc.arch = arm64  
lxc.pty.max = 1024
```