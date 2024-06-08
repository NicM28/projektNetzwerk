`cd /opt/nos`
`sudo nft add table nos`
`sudo nft add chain nos postrouting \{type nat hook postrouting priority 100 \;\}`
`sudo nft add rule nos postrouting ip saddr 10.7.0.0/16 oif wlan0 snat to z`
z = eigene ipv4

`sudo lxc-attach x` 
x = container-name

`ping 8.8.8.8`
Der ping sollte nun funktionieren
`exit`

`cd /opt/nos`
`sudo nano nos.nft`
[nos.nft](lxc-files/nos.nft)

`sudo nano nos-net`
[nos-net](lxc-files/nos-net)

sudo nano nos-net.service
[nos-net.service]

`systemctl enable /opt/nos/nos-net.service`



