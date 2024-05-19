````
# nos.nft
# -------

add table nos
add chain nos postrouting { type nat hook postrouting priority 100 ; }
add rule nos postrouting ip saddr $NOS_NET oif $WAN_IF snat to $BIND

```