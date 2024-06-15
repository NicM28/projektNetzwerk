# Neuer Container

Gemäss [[07_LXC_Setup]] einen Container namens "dnsx" aufsetzen, X mit Nummer ersetzen.

Achtung:

1. Folgendes Create-Command muss verwendet werden: `lxc-create -n dnsx -t debian+ -- -r bookworm --packages=vim-tiny,nano,iputils-ping,bind9,bind9utils,bind9-doc` X mit Nummer ersetzen.
2. Diese File sollte für config verwendet werden: [[dns config]]

# DNS einrichten

Nun müssen Master & Slave eingerichtet werden.

| domain                | A   | B     | C   | Zu hinterlegende master-datei                 |
| --------------------- | --- | ----- | --- | --------------------------------------------- |
| team07.t-nos.ch       | M   | S (M) | S   | /var/lib/bind/master/db.ch.t-nos.team07       |
| test.team07.t-nos.ch  | S   | M     | S   | /var/lib/bind/master/db.ch.t-nos.team07.test  |
| test3.team07.t-nos.ch | S   | S     | M   | /var/lib/bind/master/db.ch.t-nos.team07.test3 |


/etc/bind dort sind die config files

named.conf.local anpassen: /etc/bind/[[named.conf.local]]

Entsprechende Zonen-Dateien erstellen. (diese sind im Git abgelegt?)
SOA & NS einträge müssen vorhanden sein

Anschliessend die Master-Datei(en) in /var/lib/bind/master hinterlegen. [[db.ch.t-nos.team07.test3]]

Achtung beim Kopieren: es müssen tabulatoren oder leerschläge verwendet werden.

Die Datei [[named.conf.options]] muss auch stimmen.

Die DNS Einstellungen können mit dem Befehl `named-checkconf` geprüft werden.


Der Ordner /slave muss von Bind geschrieben werden können.
`chown bind:bind slave`


DNS kann wie folgt kontrolliert werden:

```
nslookup
> server 10.7.3.10
> set type=soa
> test3.team07.t-nos.ch.
```

