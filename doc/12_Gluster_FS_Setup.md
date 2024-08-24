Gluster Filesystem
==================

https://www.gluster.org/

Die Systeme sollten aktualisiert sein!

1. Host a und b
---------------

Eintrag im /etc/hosts

	...
	10.0.1.1	gfs1
	10.0.2.1	gfs2

Mit dem Kommando Â«pingÂ» testen!

Danach folgende Kommandos:

	apt install glusterfs-server
	mkdir -pv /srv/glfs
	service glusterd start
	service glusterd status

2. Host a
---------

Host b muss soweit bereit sein!

	gluster peer probe gfs2
	gluster peer status

3. Host b
---------

Host a muss soweit bereit sein!

	gluster peer probe gfs1
	gluster peer status

4. Host a
---------

Host b muss soweit bereit sein!

	gluster volume create home replica 2 gfs1:/srv/glfs/home gfs2:/srv/glfs/home force
	gluster volume start home

5. Host a und b
---------------

Achtung: [N] durch die entsprechende Nummer ersetzen!

	gluster volume status
	mount -t glusterfs localhost:home /var/lib/lxc/user[N]/rootfs/home