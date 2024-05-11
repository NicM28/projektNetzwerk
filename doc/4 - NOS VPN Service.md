```
# /opt/nos/nos-vpn.service

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

```
# /etc/default/nos

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
NOS_VPN_IDENTITY="/opt/nos/host-t07x"
```
x = a / b / c