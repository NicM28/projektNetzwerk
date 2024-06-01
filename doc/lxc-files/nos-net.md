```bash
#!/bin/bash
#/opt/nos/nos-net 
  
if [ -r /etc/default/nos ]; then  
   . /etc/default/nos  
fi  
  
NOS_NET=${NOS_NET:-10.0.0.0/8}  
WAN_IF=$(ip route | grep default | grep -P '(?<=dev )\S+' -o)  
BIND=$(ip -4 address show dev ${WAN_IF} primary scope global | grep -P '(?<=inet )\d+\.\d+\.\d+\.\d+' -o)
  
echo "$(basename $0): interface $WAN_IF with $BIND $1"  
  
case "$1" in  
   start)  
       echo "add rules for $(basename $0)"  
       nft -D WAN_IF=${WAN_IF} -D NOS_NET=${NOS_NET} -D BIND=${BIND} -f /opt/nos/nos.nft  
       ;;  
   stop)    
       echo "delete rules for $(basename $0)"  
       nft delete table nos  
       ;;  
   *)  
       echo "illegal command $1 like yo mom nigga for $(basename $0)"  
esac  
  
exit 0

```