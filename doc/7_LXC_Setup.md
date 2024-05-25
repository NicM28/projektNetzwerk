`sudo apt install lxc`

`cd /opt/nos`

`sudo touch lxc-debian+.patch` 
[lxc-debian+.patch](lxc-debian+.patch.md)
`sudo touch lxc-debian+.patch.sha256`
[lxc-debian+.patch](lxc-debian+.patch.sha256.md)

Zum überprüfen der hinzugefügten Dateien
`cd /opt/nos; sha256sum -c lxc-debian+.patch.sha256`
Konsole muss "OK" ausgeben

`cd /usr/share/lxc/templates`
`sudo cp -av lxc-debian+ 
`sudo patch lxc-debian+ /opt/nos/lxc-debian+.patch`

`sudo ls -l /usr/share/lxc/templates` 
lxc-debian+ muss die gleiche Berechtigung wie lxc-debian besitzen

Zum erzeugen eines Containers
`sudo lxc-create -n y -t debian+ -- -r bookworm --packages=nano,iputils-ping`
y= beliebiger Container Name 

`cd /var/lib/lxc/y
y= gewählter Container Name

`sudo nano config`
**lxc.net.0.hwaddr** nicht kopieren
x = 1 / 2 / 3
```
# Template used to create this container: /usr/share/lxc/templates/lxc-debian+
# Parameters passed to the template: -r bookworm --packages=nano,iputils-ping
# For additional config options, please look at lxc.container.conf(5)

# Uncomment the following line to support nesting containers:
#lxc.include = /usr/share/lxc/config/nesting.conf
# (Be aware this has security implications)

lxc.start.auto = 0
lxc.start.order = 99

lxc.net.0.type = veth
lxc.net.0.hwaddr = 00:16:3e:48:98:18  //m
lxc.net.0.link = br0
lxc.net.0.flags = up
lxc.net.0.ipv4.address = 10.7.x.99/16
lxc.net.0.ipv4.gateway = 10.7.x.1
lxc.net.0.veth.pair = veth99

lxc.apparmor.profile = generated
lxc.apparmor.allow_nesting = 1
lxc.rootfs.path = dir:/var/lib/lxc/x/rootfs

# Common configuration
lxc.include = /usr/share/lxc/config/debian.common.conf

# Container specific configuration
lxc.tty.max = 4
lxc.uts.name = x
lxc.arch = arm64
lxc.pty.max = 1024
```

`sudo lxc-start y`
`sudo lxc-attach y`

Eigener Host Ping möglich
`ping 10.7.x.1
`ping 8.8.8.8` Packt lose sollte 100% sein
`exit`

`ifconfig`
Benötigt wird
1. wlan0 interface
2. ipv4
3. 10.7.0.0
`sudo service lxc-net stop`

`cd /etc/default`
`sudo nano lxc-net`
Von **true** auf **false** setzten

`cd /etc/systemd/system`
`sudo ln -s /dev/null lxc-net.service`






