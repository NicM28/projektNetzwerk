```
apt update
apt install frr
```

```
# /etc/frr/frr.conf

# default to using syslog. /etc/rsyslog.d/45-frr.conf places the log in
# /var/log/frr/frr.log
#
# Note:
# FRR's configuration shell, vtysh, dynamically edits the live, in-memory
# configuration while FRR is running. When instructed, vtysh will persist the
# live configuration to this file, overwriting its contents. If you want to
# avoid this, you can edit this file manually before starting FRR, or instruct
# vtysh to write configuration to a different file.
log syslog informational

hostname host-t07x

router rip
  network br0
  network tap0

```
x = a / b / c

```
# /etc/frr/daemons

...
ripd=yes
...
```

Anschliessend frr und Netzwerk Service neustarten.
```
service frr restart
service systemd-networkd restart
```