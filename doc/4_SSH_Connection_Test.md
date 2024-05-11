Dieser Befehl kann ausgeführt werden, sobald unser SSH-Key von Bruno hinzugefügt wurde. Damit können wir die VPN verbindung testen.

`ssh -p 1022 -i /opt/nos/host-t07x -o Tunnel=ethernet -w 0 -T teams@vpn.t-nos.ch`