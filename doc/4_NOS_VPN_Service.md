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
ExecStart=/usr/bin/ssh $NOS_VPN_PORT -i $NOS_VPN_IDENTITY -o Tunnel=ethernet -w $NOS_VPN_TAPNR -T $NOS_VPN_SERVER  
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
NOS_VPN_PORT="-p 1022"$  
  
# SSH Identity-File (private key) for authentication  
NOS_VPN_IDENTITY="/opt/nos/host-t07x"

```
x = a / b / c

`systemctl enable /opt/nos/nos-vpn.service`