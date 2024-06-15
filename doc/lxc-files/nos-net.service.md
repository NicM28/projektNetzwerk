```
# /opt/nos/nos-net.service

[Unit]
Description=Network (NAT) for LXC (NOS)
After=lxc.service network-online.target
Wants=lcx.service network-online.target
ConditionPathExists=!/etc/nos_not_to_be_run

[Service]
Type=oneshot
EnvironmentFile=-/etc/default/nos
RemainAfterExit=yes
ExecStart=/bin/bash /opt/nos/nos-net start
ExecStop=/bin/bash /opt/nos/nos-net stop

[Install]
WantedBy=multi-user.target
```