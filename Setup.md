# Installieren von Raspberry OS

1. Download [Raspberry OS](https://www.raspberrypi.com/software/)
2. Exe ausführen
3. SD Karte auswählen
4. OS wählen (Raspberry Pi OS Lite 64 Bit)
	weiter
5. Einstellungen bearbeiten
6. Hostname ändern in: host-t07x > x= je nach Einteilung innerhalb des Teams a, b oder c
7. Die weiteren Abschnitte einrichte 
8. Zum Tab Dienste wechseln und SSH aktivieren
9. OS brennen

## Verbinden mit Raspberry

1. SD Karte in Raspberry einfügen
2. Raspberry an Pingen `ping -4 host-t07x`
3. Über ssh mit Raspberry verbinden `ssh user@ip`

## Raspberry Einstellungen

- Copy bashrc file `cp bashrc bashrc-SAVE`
- bashrc file bearbeiten je nach Präferenzen
## Swap Größe ändern

1. `nano /etc/dphys-swapfile` > dphys-swapfile öffnen
2. swapfactor auf 1 ändern
3. swapsize kommentieren
4. file speichern
5. `service dphys-swapfile restart`

## Raspberry Config anpassen

1. `raspi-config` in die Konsole eingeben
2. interface Options auswählen
3. Serial Port aktivieren


## Raspberry Netzwerk-Konfig anpassen

zwei Files in /etc/systemd/network erstellen:

10-br0.netdev
```
[NetDev]
Description=Bridge for LXC-Containers
Name=br0
Kind=bridge
```

10-br0.network
```
[Match]
Name=br0

[Network]
Address=10.7.X.1/16
DHCP=no
LinkLocalAddressing=no
IPForward=ipv4
```

X => a = 1, b = 2, c = 3

## Schlüsselpaar 

### Generieren

1. Ordner erstellen: /opt/nos
2. darin ausführen: ```sudo ssh-keygen```
3. beim Filename ```host-t07x``` angeben (x = a/b/c)
4. keine passphrase verwenden

zwei Dateien wurden generiert

### Hochladen

1. Public Key vom Raspy herunterladen
2. Umbenennen zu Textdatei host-t07a.txt
3. Diese Datei bei Bruno hochladen: https://elad.ch/
   Gruppen -> L-TIN-22-T-a -> Ordner

## port zeugs

Dieser Befehl kann ausgeführt werden, sobald unser SSH-Key von Bruno hinzugefügt wurde.
`ssh -p 1022 -i host-t07x -o Tunnel=ethernet -w 0 -T teams@vpn.t-nos.ch`