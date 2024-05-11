```
# /etc/systemd/network/10-br0.netdev

[NetDev]
Description=Bridge for LXC-Containers
Name=br0
Kind=bridge
```

```
# /etc/systemd/network/10-br0.network

[Match]
Name=br0

[Network]
Address=10.7.X.1/16
DHCP=no
LinkLocalAddressing=no
IPForward=ipv4
```

x => a = 1, b = 2, c = 3