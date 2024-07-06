DNS Einträge richtig machen
```
# /etc/resolv.conf
nameserver 10.7.1.10
nameserver 10.7.2.10
nameserver 10.7.3.10
```

Installation
------------

	apt install samba nullmailer

Konfiguration
-------------

Backend für LDAP konfigurieren: /etc/samba/smb.conf

	...
	netbios name = TEAM00
	workgroup    = TEAMS0
	...
	obey pam restrictions = yes
	passdb backend = ldapsam:ldap://10.0.1.11
	ldap suffix = dc=team00,dc=t-nos,dc=ch
	ldap user suffix =
	ldap group suffix = ou=Groups
	ldap machine suffix = ou=Computers
	ldap admin dn = uid=admin,ou=system
	ldap ssl = off
	...
	[homes]
	...
	read only = no
	...

Administrationpasswort setzten: (auf userX)
**Hier muss das Admin Passwort vom ldap verwendet werden**

	smbpasswd -W

Dienste neu starten:

	service smbd restart
	service nmbd restart

Konto fÃ¼r Benutzer Â«checkÂ» aktivieren:

	smbpasswd -a check

Tests:

	net getlocalsid
	net -U check share list -l