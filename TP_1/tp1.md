## TP1

🌞 Adresses IP de ta machine

- L'adresse IP sur la carte reseau Wifi : 10.33.77.160
- L'adresse IP sur la carte reseaux ethernet : je ne suis pas connecte 

🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...

- L'adresse IP de la passerelle du réseau local : 10.33.79.254
- L'adresse IP du serveur DNS que connaît mon PC : 8.8.8.8 / 1.1.1.1
- L'adresse IP du serveur DHCP que connaît mon PC : 10.33.79.254

🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine : Il y a un pare-feu (Kaspersky)

## Utiliser le réseau

🌞 Envoie un ping vers ...
* toi-même : 
  * PS C:\Users\yarki> ping 10.33.77.160

Pinging 10.33.77.160 with 32 bytes of data:
Reply from 10.33.77.160: bytes=32 time<1ms TTL=128
Reply from 10.33.77.160: bytes=32 time<1ms TTL=128
Reply from 10.33.77.160: bytes=32 time<1ms TTL=128
Reply from 10.33.77.160: bytes=32 time<1ms TTL=128

Ping statistics for 10.33.77.160:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
* vers l'adresse IP 127.0.0.1 :
    * PS C:\Users\yarki> ping 127.0.0.1

Pinging 127.0.0.1 with 32 bytes of data:
Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
Reply from 127.0.0.1: bytes=32 time<1ms TTL=128

Ping statistics for 127.0.0.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

* ma passerelle :
    * PS C:\Users\yarki> ping 10.33.79.254

Pinging 10.33.79.254 with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 10.33.79.254:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
* mon pote :
    * PS C:\Users\yarki> ping 10.33.76.111

Pinging 10.33.76.111 with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 10.33.76.111:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),

* un site d'internet : 
    * PS C:\Users\yarki> ping www.thinkerview.com

Pinging www.thinkerview.com [188.114.96.7] with 32 bytes of data:
Reply from 188.114.96.7: bytes=32 time=17ms TTL=55
Reply from 188.114.96.7: bytes=32 time=16ms TTL=55
Reply from 188.114.96.7: bytes=32 time=15ms TTL=55
Reply from 188.114.96.7: bytes=32 time=16ms TTL=55

Ping statistics for 188.114.96.7:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 15ms, Maximum = 17ms, Average = 16ms

🌞 Faire une requête DNS à la main
* www.thinkview.com
    * PS C:\Users\yarki> Resolve-DnsName www.thinkerview.com

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
www.thinkerview.com                            AAAA   300   Answer     2a06:98c1:3121::7
www.thinkerview.com                            AAAA   300   Answer     2a06:98c1:3120::7
www.thinkerview.com                            A      300   Answer     188.114.97.7
www.thinkerview.com                            A      300   Answer     188.114.96.7

* www.wikileaks.org
    * Name       : wikileaks.org
    * QueryType  : A
    * TTL        : 1644
    * Section    : Answer
    * IP4Address : 51.159.197.136

* www.torproject.org
    * www.torproject.org                             A      77    Answer     204.8.99.144
    * www.torproject.org                             A      77    Answer     95.216.163.36
    * www.torproject.org                             A      77    Answer     116.202.120.166
    * www.torproject.org                             A      77    Answer     204.8.99.146
    * www.torproject.org                             A      77    Answer     116.202.120.165

    ## Sniffer les reseaux

🌞 J'attends dans le dépôt git de rendu un fichier ping.pcap

[ping](icmp-only.pcap)

## Network scanning et adresses IP

🌞 Effectue un scan du réseau auquel tu es connecté

* nmap -sn 10.33.77.160
    * Starting Nmap 7.95 ( https://nmap.org ) at 2024-10-02 12:04 Romanya Yaz Saati
Nmap scan report for 10.33.77.160
Host is up.
Nmap done: 1 IP address (1 host up) scanned in 0.30 seconds

🌞 Changer d'adresse IP

* Wireless LAN adapter Wi-Fi:

    * Connection-specific DNS Suffix  . :
    * Link-local IPv6 Address . . . . . : fe80::69ed:e565:72a8:37fd%16
    * IPv4 Address. . . . . . . . . . . : 
    192.168.1.20
    * Subnet Mask . . . . . . . . . . . : 
    255.255.255.0
    * Default Gateway . . . . . . . . . : 
    192.168.1.1
