# Neuer Container aufsetzen

Als nächstes sollte der LDAP Container aufgesetzt werden.

Gemäss [[07_LXC_Setup]] einen Container namens "ldapx" aufsetzen, X mit Nummer ersetzen.

Achtung:

1. Folgendes Create-Command muss verwendet werden: `lxc-create -n ldapx -t debian+ -- -r bookworm --packages=vim-tiny,nano` X mit Nummer ersetzen.
2. Diese File sollte für config verwendet werden: [[ldap config]]
3. DNS Einträge richtig machen
```
# /etc/resolv.conf
nameserver 10.7.1.10
nameserver 10.7.2.10
nameserver 10.7.3.10
```
4. Anschliessend Installation auf den ldap container nach Anleitung [https://elad.ch/gitblit/blob/L-TIN-22-T-a!4-NOS!team00a.git/master/LDAP-Apache-Directory.md]
5. Nicht vergessen, den apacheds zu starten! `service apacheds start`

Via Apache Directory Studio einloggen:
1. Route Eintrag auf Laptop erstellen
```sh
# Linux
ip route add 10.7.0.0/16 via [raspi ip]

# Windows
route add 10.7.0.0 mask 255.255.0.0 [raspi ip]
```
2. Connection erstellen in Apache Directory Studio
```
Hostname: 10.7.x.11
Port: 10389
User: uid=admin,ou=system
Password: secret
```

Über Apache Directory Studio eine neue Partition anlegen:
1. Rechtsklick auf die Connection
2. Open Configuration
3. Tab Partitions auswählen
4. Neue Partition hinzufügen
	ID = Team07
	Suffix = dc=team07,dc=t-nos,dc=ch
5. Auf der Partition das Attribut description setzen
6. Tab Replication auswählen
7. Neue Replikation hinzufügen und mit Standarteinstellungen speichern
8. Bei ou=schema reloaden
9. cn=nis & cn=samba anwählen und m-disabled auf FALSE ändern
10. ldap neu starten

Check Account in unserem Namespace erstellen
```
Object Classes: inetOrgPerson, posixAccount, shadowAccount
cn: check
gecos: check
gidNumber: 100
uidNumber: 1000
homeDirectory: /home/check
loginShell: /bin/bash
uid: check
userPassword: checker (CRYPT-SHA-512)
```