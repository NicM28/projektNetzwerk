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

## tap0 zeugs

`cp 10-br0.network 10-tap0.network`

```
# 10-tap0.network  
  
[Match]  
Name=tap0  
   
[Network]  
Address=10.10.7.1/16  
DHCP=no  
LinkLocalAddressing=no  
IPForward=ipv4
```

## nos VPN Service

neues File:
`/opt/nos/nos-vpn.service`

```
[Unit]  
After=network.target network-online.target auditd.service  
Wants=network-online.target  
ConditionPathExists=!/etc/nos_not_to_be_run  
  
[Service]  
Type=simple  
Environment="NOS_VPN_TAPNR=0"  
EnvironmentFile=-/etc/default/nos  
ExecStart=/usr/bin/ssh $NOS_VPN_PORT -i $NOS_VPN_IDENTITY -  
o Tunnel=ethernet -w $NOS_VPN_TAPNR -T $NOS_VPN_SERVER  
KillMode=process  
Restart=on-failure  
RestartPreventExitStatus=255  
  
[Install]  
WantedBy=multi-user.target
```

neues File:
`/etc/default/nos`

Achtung, ist noch nicht korrekt, Werte müssen individualisiert werden.

```
# Configuration NOS  
# =================  
  
# VPN  
# ---  
  
# SSH username@hostname  
#NOS_VPN_SERVER="teams@vpn.t-nos.ch"  
NOS_VPN_SERVER="teams@185.142.213.23"  
  
# SSH Port  
NOS_VPN_PORT="-p 1022"$  
  
# SSH Identity-File (private key) for authentication  
NOS_VPN_IDENTITY="/opt/nos/host-t07c"
```