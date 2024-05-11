```
#/etc/systemd/network/10-eth0.network

[Match]
Name=eth0

[Network]
DHCP=no
LinkLocalAddressing=no
Bridge=br0
```