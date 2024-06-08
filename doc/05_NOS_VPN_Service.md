Damit wir nicht die SSH Verbindung nicht jedesmal von Hand öffnen müssen, registrieren wir das ganze als Service und aktivieren diesen damit er automatisch gestartet wird.

```
# /opt/nos/nos-vpn.service

[Unit]  
Description=VPN over SSH for NOS
Documentation=man:ssh(8) man:ssh_config(5)
After=network.target network-online.target auditd.service
Wants=network-online.target
ConditionPathExists=!/etc/nos_not_to_be_run
  
[Service]  
Type=simple  
Environment="NOS_VPN_TAPNR=0"  
EnvironmentFile=-/etc/default/nos  
ExecStart=/usr/bin/ssh -p $NOS_VPN_PORT -i $NOS_VPN_IDENTITY -o Tunnel=ethernet -w $NOS_VPN_TAPNR -T $NOS_VPN_SERVER  
KillMode=process
Restart=on-failure
RestartPreventExitStatus=255
  
[Install]
WantedBy=multi-user.target
```

```
# /etc/default/nos

# Configuration NOS  
# =================  

NOS_NET=10.0.0.0/16

# Team
NOS_TEAM_NO=7
NOS_TEAM_MEMBER_NO=1 # <- Hier Teilnehmernummer angeben

MEMBERS=(a b c)
NOS_TEAM_MEMBER=${MEMBERS[$(($NOS_TEAM_MEMBER_NO - 1))]}
  
# VPN  
# ---  
  
# SSH username@hostname  
# NOS_VPN_SERVER="teams@vpn.t-nos.ch"  
NOS_VPN_SERVER="teams@185.142.213.23"  
  
# SSH Port  
NOS_VPN_PORT=1022
  
# SSH Identity-File (private key) for authentication  
NOS_VPN_IDENTITY="/opt/nos/host-t07x"

```
x = a / b / c

Das erste mal muss das Zertifikat geladen werden. Dazu öffnen wir eine ssh verbindung zum server und bestätigen mit `yes` dass wir den fingeprint speichern möchten. Bei der Passwort abfrage können wir den Befehl abbrechen.

`ssh -p 1022 teams@185.142.213.23`

Anschliessend kann der Service dauerhaft enabled werden.

`systemctl enable /opt/nos/nos-vpn.service`

Der VPN Service kann mit folgendem Befehl gestartet, neugestartet und abgefragt werden.

```
service nos-vpn start
service nos-vpn restart
service nos-vpn status
```