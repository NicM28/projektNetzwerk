# Neuer Container

Gemäss [[7_LXC_Setup]] einen Container namens "dnsx" aufsetzen, X mit Nummer ersetzen.

Achtung:

1. Folgendes Create-Command muss verwendet werden: `lxc-create -n dnsx -t debian+ -- -r bookworm --packages=vim-tiny,nano,iputils-ping,bind9,bind9utils,bind9-doc` X mit Nummer ersetzen.
2. Diese File sollte für config verwendet werden: [[config]]

# DNS einrichten

Nun müssen Master & Slave eingerichtet werden.

| domain                | A   | B     | C   |
| --------------------- | --- | ----- | --- |
| team07.t-nos.ch       | M   | S (M) | S   |
| test.team07.t-nos.ch  | S   | M     | S   |
| test3.team07.t-nos.ch | S   | S     | M   |


/etc/bind dort sind die config files

named.conf.local anpassen: /etc/bind/[[named.conf.local]]

Entsprechende Zonen-Dateien erstellen. (diese sind im Git abgelegt?)
SOA & NS einträge müssen vorhanden sein
