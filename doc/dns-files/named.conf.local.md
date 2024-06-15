```bind
// /etc/bind/namd.conf.local
// Do any local configuration here  
//  
  
// Consider adding the 1918 zones here, if they are not used in y>  
// organization  
//include "/etc/bind/zones.rfc1918";  
  
zone "test3.team07.t-nos.ch." {  
       type master;  
       file "/var/lib/bind/master/db.ch.t-nos.team07.test3";  
       allow-transfer { 10.7.1.10; 10.7.2.10; };  
};  
  
zone "team07.t-nos.ch." {  
       type slave;  
       file "/var/lib/bind/slave/db.ch.t-nos.team07";  
       masters { 10.7.1.10; };  
};  
  
zone "test.team07.t-nos.ch." {  
       type slave;  
       file "/var/lib/bind/slave/db.ch.t-nos.team07.test";  
       masters { 10.7.2.10; };  
};
```