````
#!/bin/bash

if [ -r /etc/default/nos ]; then
  . /etc/default/nos
fi

NOS_NET=${NOS_NET:-10.0.0.0/8}
WAN_IF=$(ip route | grep default | grep -P '(?<=dev )\S+' -o)
BIND=$(ip -4 address show dev ${WAN_IF} primary scope global | grep -P '(?<=inet )\d+\.\d+\.\d+\.\d+' -o)

echo "$(basename $0): interface $WAN_IF with $BIND $1"

case "$1" in
        start)
         ;;
        stop)
         ;;
        *)
          echo "illegal command $1 for $(basename $0)"
         ;;
esac

exit 0

```