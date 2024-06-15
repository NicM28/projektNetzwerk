# Neuer Container aufsetzen

Als nächstes sollte der LDAP Container aufgesetzt werden.

Gemäss [[07_LXC_Setup]] einen Container namens "ldapx" aufsetzen, X mit Nummer ersetzen.

Achtung:

1. Folgendes Create-Command muss verwendet werden: `lxc-create -n ldapx -t debian+ -- -r bookworm --packages=vim-tiny,nano` X mit Nummer ersetzen.
2. Diese File sollte für config verwendet werden: [[ldap config]]