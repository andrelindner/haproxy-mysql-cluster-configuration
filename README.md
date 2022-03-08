# HAProxy - Konfiguration  

## Pakete installieren (Ubuntu)  
- sudo apt-get update  
- sudo apt-get install haproxy  
  
  
## /etc/haproxy/haproxy.cnf 
Damit der HAProxy die Cluster-Knoten ansprechen kann, müssen diese in der HAProxy Konfiguration hinterlegt werden.  
  
listen mysql-cluster  
 bind    :3300  
 mode    tcp  
 maxconn 150  
 timeout connect 10s  
 timeout client 60s  
 timeout server 60s  
 balance roundrobin  
 timeout connect 10s  
 timeout server 60s  
 server server1.xyz.de 192.168.1.1:3306 maxconn 50 check  
 server server2.xyz.de 192.168.1.2:3306 maxconn 50 check  
 server server3.xyz.de 192.168.1.3:3306 maxconn 50 check  
  
Die Statistik des HAProxy kann über eine Weboberfläche eingesehen werden. Die Konfiguration der Weboberfläche kann dann wie folgt erfolgen. Das Verzeichnis ist geschützt.  
  
listen stats  
 bind *:8080  
 mode http  
 stats enable  
 timeout connect 10s  
 timeout client 1m  
 timeout server 1m  
 stats uri /stats  
 stats refresh 30s  
 stats auth administrator:passwort  
