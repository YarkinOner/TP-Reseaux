# TP6 : Des bo services dans des bo LANs

## 2. Marche à suivre

☀️ Prouvez que...

une machine du LAN1 peut joindre internet (ping un nom de domaine)

```powershell
[oyarkin@dhcp ~]$ ping www.google.com
PING www.google.com (142.250.201.36) 56(84) bytes of data.
64 bytes from mrs08s20-in-f4.1e100.net (142.250.201.36): icmp_seq=1 ttl=112 time=21.3 ms
64 bytes from mrs08s20-in-f4.1e100.net (142.250.201.36): icmp_seq=2 ttl=112 time=20.1 ms
64 bytes from mrs08s20-in-f4.1e100.net (142.250.201.36): icmp_seq=3 ttl=112 time=21.0 ms
64 bytes from mrs08s20-in-f4.1e100.net (142.250.201.36): icmp_seq=4 ttl=112 time=21.6 ms
64 bytes from mrs08s20-in-f4.1e100.net (142.250.201.36): icmp_seq=5 ttl=112 time=21.6 ms
^C
--- www.google.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4011ms
rtt min/avg/max/mdev = 12.341/14.100/15.643/0.556 ms
```

une machine du LAN2 peut joindre internet (ping nom de domaine)

```powershell
[oyarkin@dns ~]$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=53 time=20.6 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=53 time=20.3 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=53 time=24.2 ms
^C64 bytes from 172.67.74.226: icmp_seq=4 ttl=53 time=79.8 ms

--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3008ms
rtt min/avg/max/mdev = 20.345/36.212/79.788/25.203 ms
```

```powershell
[oyarkin@dns ~]$ ping 10.6.1.253
PING 10.6.1.253 (10.6.1.253) 56(84) bytes of data.
64 bytes from 10.6.1.253: icmp_seq=1 ttl=63 time=4.44 ms
64 bytes from 10.6.1.253: icmp_seq=2 ttl=63 time=2.54 ms
64 bytes from 10.6.1.253: icmp_seq=3 ttl=63 time=3.32 ms
^C
--- 10.6.1.253 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2007ms
rtt min/avg/max/mdev = 2.543/3.434/4.441/0.779 ms
```

# II. LAN clients

☀️ Prouvez que...

```powershell
oyarkin@client3:~/Desktop$ sudo nano /etc/netplan/01-netcfg.yaml
[sudo] password for oyarkin: 

oyarkin@client3:~/Desktop$ sudo netplan apply

** (generate:3777): WARNING **: 12:26:52.202: Permissions for /etc/netplan/01-netcfg.yaml are too open. Netplan configuration should NOT be accessible by others.

** (process:3776): WARNING **: 12:26:52.529: Permissions for /etc/netplan/01-netcfg.yaml are too open. Netplan configuration should NOT be accessible by others.

** (process:3776): WARNING **: 12:26:52.623: Permissions for /etc/netplan/01-netcfg.yaml are too open. Netplan configuration should NOT be accessible by others.

moyarkin@client3:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:02:ef:f4 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s8
       valid_lft 599sec preferred_lft 599sec
    inet6 fe80::a00:27ff:fe02:eff4/64 scope link 
       valid_lft forever preferred_lft forever
3: mpqemubr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 52:54:00:a3:35:7f brd ff:ff:ff:ff:ff:ff
    inet 10.237.56.1/24 brd 10.237.56.255 scope global mpqemubr0
       valid_lft forever preferred_lft forever

oyarkin@client3:~/Desktop$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
       DNS Servers: 1.1.1.1
        DNS Domain: srv.world

Link 3 (mpqemubr0)
    Current Scopes: none
         Protocols: -DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported

oyarkin@client3:~/Desktop$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=53 time=25.7 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=53 time=21.1 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1056ms
rtt min/avg/max/mdev = 21.115/23.389/25.664/2.274 ms

oyarkin@client3:~/Desktop$ ip route show
default via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100 
1.1.1.1 via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100 
10.6.1.0/24 dev enp0s3 proto kernel scope link src 10.6.1.37 metric 100 
10.6.1.254 dev enp0s3 proto dhcp scope link src 10.6.1.37 metric 100 
10.237.56.0/24 dev mpqemubr0 proto kernel scope link src 10.237.56.1 linkdown 

oyarkin@client3:~/Desktop$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=53 time=19.5 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=53 time=22.1 ms
^C
--- 1.1.1.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 19.472/20.776/22.080/1.304 ms
```
# III. LAN serveurzzzz

☀️ Déterminer sur quel port écoute le serveur NGINX

```powershell
[oyarkin@web ~]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=5473,fd=6),("nginx",pid=5472,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=5473,fd=7),("nginx",pid=5472,fd=7))
```

☀️ Ouvrir ce port dans le firewall

```powershell
[oyarkin@web ~]$ sudo firewall-cmd --permanent --add-port=80/tcp
success
[oyarkin@web ~]$ sudo firewall-cmd --reload
success
```

☀️ Visitez le site web !

```powershell
oyarkin@client3:~/Desktop$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
      
      html {
        height: 100%;

```

## 4. Analyse du service
☀️ Déterminer sur quel(s) port(s) écoute le service BIND9

```powershell
[oyarkin@dns ~]$ sudo ss -lnpt | grep 53
LISTEN 0      4096       127.0.0.1:953       0.0.0.0:*    users:(("named",pid=11603,fd=28))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=11603,fd=25))
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=11603,fd=22))
LISTEN 0      4096           [::1]:953          [::]:*    users:(("named",pid=11603,fd=29))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=11603,fd=27))
```

☀️ Ouvrir ce(s) port(s) dans le firewall

```powershell
[oyarkin@dns ~]$ sudo firewall-cmd --permanent --add-port=53/tcp
success
[oyarkin@dns ~]$ sudo firewall-cmd --reload
success
```

## 5. Tests manuels
☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps

```powershell
[oyarkin@dns ~]$ dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63021
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 7c5ff46ed845160b01000000671a07b50bdb88d723890895 (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 6 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Thu Oct 24 10:39:17 CEST 2024
;; MSG SIZE  rcvd: 83

[oyarkin@dns ~]$ dig dns.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 37503
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: ce8f29a42cc2ace001000000671a07c5dab7b61560afec8e (good)
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Thu Oct 24 10:39:33 CEST 2024
;; MSG SIZE  rcvd: 83

[oyarkin@dns ~]$ dig ynov.com @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 25070
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 8c4c423af388e35101000000671a07cb7464809464055b3b (good)
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       104.26.11.233

;; Query time: 245 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Thu Oct 24 10:39:39 CEST 2024
;; MSG SIZE  rcvd: 113

[oyarkin@dns ~]$ dig -x 10.6.2.11 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 56627
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 05c22eb642d255d001000000671a07d5c82d0c1c1726dbef (good)
;; QUESTION SECTION:
;11.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.

;; Query time: 13 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Thu Oct 24 10:39:49 CEST 2024
;; MSG SIZE  rcvd: 103

[oyarkin@dns ~]$ dig -x 10.6.2.12 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12546
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: f5625a313488933d01000000671a07dafb758708b50f6061 (good)
;; QUESTION SECTION:
;12.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Thu Oct 24 10:39:54 CEST 2024
;; MSG SIZE  rcvd: 103
```

☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1

```powershell
oyarkin@client3:~/Desktop$ dig web.tp6.b1

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web.tp6.b1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 9989
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;web.tp6.b1.			IN	A

;; AUTHORITY SECTION:
.			86400	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2024102400 1800 900 604800 86400

;; Query time: 39 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Thu Oct 24 10:48:15 CEST 2024
;; MSG SIZE  rcvd: 114

```

☀️ Capturez une requête DNS et la réponse de votre serveur

```powershell
oyarkin@client3:~/Desktop$ sudo tcpdump -w dns_capture.pcap -i enp0s3 port 53
tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
^C31 packets captured
31 packets received by filter
0 packets dropped by kernel
oyarkin@client3:~/Desktop$ ^C
oyarkin@client3:~/Desktop$ tcpdump -r dns_capture.pcap
reading from file dns_capture.pcap, link-type EN10MB (Ethernet), snapshot length 262144
10:54:31.348354 IP client3.44321 > 10.6.2.12.domain: 65456+ [1au] A? web.tp6.b1. (51)
10:54:31.352243 IP client3.43912 > 10.6.2.12.domain: 65456+ [1au] A? web.tp6.b1. (51)
10:54:31.356764 IP client3.59506 > 10.6.2.12.domain: 65456+ [1au] A? web.tp6.b1. (51)
10:56:01.847029 IP client3.47808 > one.one.one.one.domain: 14247+ [1au] A? cdimage.ubuntu.com. (47)
10:56:01.847673 IP client3.36315 > one.one.one.one.domain: 46091+ [1au] AAAA? cdimage.ubuntu.com. (47)
10:56:01.859904 IP client3.56292 > one.one.one.one.domain: 62804+ [1au] A? cloud-images.ubuntu.com. (52)
10:56:01.863372 IP client3.56217 > one.one.one.one.domain: 21630+ [1au] AAAA? cloud-images.ubuntu.com. (52)
10:56:01.871223 IP one.one.one.one.domain > client3.47808: 14247 3/0/1 A 91.189.91.124, A 91.189.91.123, A 185.125.190.37 (95)
10:56:01.881995 IP one.one.one.one.domain > client3.56292: 62804 2/0/1 A 185.125.190.37, A 185.125.190.40 (84)
10:56:01.888968 IP one.one.one.one.domain > client3.36315: 46091 3/0/1 AAAA 2001:67c:1562::28, AAAA 2001:67c:1562::25, AAAA 2620:2d:4000:1::17 (131)
10:56:01.976502 IP one.one.one.one.domain > client3.56217: 21630 2/0/1 AAAA 2620:2d:4000:1::17, AAAA 2620:2d:4000:1::1a (108)
10:56:14.155968 IP client3.54219 > one.one.one.one.domain: 27182+ [1au] A? contile.services.mozilla.com. (57)
10:56:14.158575 IP client3.44554 > one.one.one.one.domain: 65088+ [1au] HTTPS? contile.services.mozilla.com. (57)
10:56:14.162819 IP client3.46100 > one.one.one.one.domain: 49107+ [1au] AAAA? contile.services.mozilla.com. (57)
10:56:14.176523 IP one.one.one.one.domain > client3.54219: 27182 1/0/1 A 34.117.188.166 (73)
10:56:14.179970 IP one.one.one.one.domain > client3.44554: 65088 0/1/1 (138)
10:56:14.183825 IP one.one.one.one.domain > client3.46100: 49107 0/1/1 (138)
10:56:16.649795 IP client3.55274 > one.one.one.one.domain: 35598+ [1au] HTTPS? temuaffiliateprogram.pxf.io. (56)
10:56:16.656254 IP client3.41585 > one.one.one.one.domain: 43950+ [1au] A? temuaffiliateprogram.pxf.io. (56)
10:56:16.666569 IP client3.59685 > one.one.one.one.domain: 27420+ [1au] AAAA? temuaffiliateprogram.pxf.io. (56)
10:56:16.666940 IP client3.37346 > one.one.one.one.domain: 21467+ [1au] A? fr.hotels.com. (42)
10:56:16.676029 IP one.one.one.one.domain > client3.55274: 35598 0/1/1 (140)
10:56:16.680752 IP client3.48596 > one.one.one.one.domain: 32618+ [1au] AAAA? fr.hotels.com. (42)
10:56:16.704634 IP one.one.one.one.domain > client3.41585: 43950 1/0/1 A 35.201.76.231 (72)
10:56:16.704635 IP one.one.one.one.domain > client3.59685: 27420 0/1/1 (140)
10:56:16.704635 IP one.one.one.one.domain > client3.37346: 21467 3/0/1 CNAME ipv6-global.hotels.com.edgekey.net., CNAME e10109.dscx.akamaiedge.net., A 23.203.162.75 (143)
10:56:16.704635 IP one.one.one.one.domain > client3.48596: 32618 4/0/1 CNAME ipv6-global.hotels.com.edgekey.net., CNAME e10109.dscx.akamaiedge.net., AAAA 2a02:26f0:b80:693::277d, AAAA 2a02:26f0:b80:69d::277d (183)
10:56:16.735090 IP client3.55314 > one.one.one.one.domain: 9858+ [1au] HTTPS? e10109.dscx.akamaiedge.net. (55)
10:56:16.762626 IP one.one.one.one.domain > client3.55314: 9858 0/1/1 (119)
10:56:50.875477 IP client3.60575 > 10.6.2.12.domain: 33523+ [1au] A? web.tp6.b1. (51)
10:56:50.880533 IP 10.6.2.12.domain > client3.60575: 33523* 1/0/1 A 10.6.2.11 (83)

```

## 3. Serveur DHCP

☀️ Créez un nouveau client client2.tp6.b1 vitefé

```powershell
oyarkin@yarki-VirtualBox:~/Desktop$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
       DNS Servers: 10.6.2.12
        DNS Domain: srv.world

```