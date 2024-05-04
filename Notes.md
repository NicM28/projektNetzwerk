befehle
nmcli dev 
cd /etc/systemd/network

touch 10-br0.netdev
	# 10-br0.netdev
	# ==========

	[NetDev]
	Description=Bridge for LXC-Containers
	Name=br0
	Kind=bridge

touch 10-br0.network
	# 10-br0.network
	# ==========
	[Match]
	Name=br0

	[Network]
	Address=10.07.x.1/16
	DHCP=no
	LinkLocalAddressing=no
	IPForward=ipv4

systemctl enable systemd-networkd
system systemd-networkd start
ifconfig br0 // zum checken ob bridge vorhanden ist

ssh schlüssel generieren

cd /opt
mkdir /nos
cd nos
ssh-keygen
pubkey hochladen auf olat
`ssh -p 1022 -i host-t07b -o Tunnel=ethernet -w 0 -T teams@vpn.t-nos.ch`
ausführen
zweite shell öffnen und `tap0` eingeben 
 
