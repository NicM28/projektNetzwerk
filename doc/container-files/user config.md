```
# Template used to create this container: /usr/share/lxc/templates/lxc-debian+
# Parameters passed to the template: -r bookworm --packages=vim-tiny,nano
# For additional config options, please look at lxc.container.conf(5)

# Uncomment the following line to support nesting containers:
#lxc.include = /usr/share/lxc/config/nesting.conf
# (Be aware this has security implications)

lxc.net.0.type = veth
# lxc.net.0.hwaddr = 00:16:3e:bb:d6:5d
lxc.net.0.link = br0
lxc.net.0.flags = up
lxc.net.0.ipv4.address = 10.7.x.12/16 # <---------
lxc.net.0.ipv4.gateway = 10.7.x.1 # <---------
lxc.net.0.veth.pair = veth12

lxc.apparmor.profile = generated
lxc.apparmor.allow_nesting = 1
lxc.rootfs.path = dir:/var/lib/lxc/userx/rootfs # <---------

# Common configuration
lxc.include = /usr/share/lxc/config/debian.common.conf

# Container specific configuration
lxc.tty.max = 4
lxc.uts.name = userx # <---------
lxc.arch = arm64
lxc.pty.max = 1024
```