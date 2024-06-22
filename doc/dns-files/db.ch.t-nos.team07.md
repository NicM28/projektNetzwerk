```
; /var/lib/bind/master/db.ch.t-nos.team07

$TTL 60  
@ IN SOA ns1.team07.t-nos.ch. admin.team07.t-nos.ch. (  
       2024052504 ; Serial  
       1d ; Refresh  
       2h ; Retry  
       6w ; Expire  
       60 ; Negative Cache TTL  
)  
  
@               IN      NS      ns1.team07.t-nos.ch.
@               IN      NS      ns2.team07.t-nos.ch.
@               IN      NS      ns3.team07.t-nos.ch.
  
@               IN      TXT     "Hello this is blank"

test IN NS ns1
test IN NS ns2
test IN NS ns3

test3 IN NS ns1
test3 IN NS ns2
test3 IN NS ns3

host-t07a       IN      A       10.7.1.1
host-t07b       IN      A       10.7.2.1
host-t07c       IN      A       10.7.3.1
  
ns1             IN      A       10.7.1.10
ns2             IN      A       10.7.2.10
ns3             IN      A       10.7.3.10
  
dns1            IN      A       10.7.1.10
dns2            IN      A       10.7.2.10
dns3            IN      A       10.7.3.10
  
ldap1           IN      A       10.7.1.11
ldap2           IN      A       10.7.2.11
ldap3           IN      A       10.7.3.11
  
user1           IN      A       10.7.1.12
user2           IN      A       10.7.2.12
user3           IN      A       10.7.3.12

; Service
_ldap._tcp	    IN	    SRV	    10 50 389 ldap1
                IN	    SRV	    10 50 389 ldap2
		        IN	    SRV	    10 50 389 ldap3
```