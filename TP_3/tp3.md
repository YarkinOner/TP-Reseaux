## ARP Basics

☀️ Affichez l'adresse MAC de votre carte WiFi
*   C8-94-02-F8-AB-97

☀️ Affichez votre table ARP
```
PS C:\Users\yarki> arp -a
```
☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école
* la passerelle : 10.33.79.254
*   l'adresse MAC :
```
10.33.79.254          7c-5a-1c-d3-d8-76     dynamic
```
☀️ Supprimez la ligne qui concerne la passerelle
```
PS C:\WINDOWS\system32> arp -d 10.33.79.254
```
☀️ Prouvez que vous avez supprimé la ligne dans la table ARP
```
10.33.79.210          14-4f-8a-75-cb-50     dynamic
  10.33.79.230          10-68-38-3f-98-67     dynamic
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamic
  224.0.0.2             01-00-5e-00-00-02     static
  ```
  la commande : arp -d 10.33.79.254
  ```
   10.33.78.113          9e-55-25-75-8b-97     dynamic
  10.33.78.165          c0-35-32-e6-90-05     dynamic
  10.33.79.210          14-4f-8a-75-cb-50     dynamic
  10.33.79.230          10-68-38-3f-98-67     dynamic
  224.0.0.2             01-00-5e-00-00-02     static
  ```
  ☀️ Wireshark
  * capture arp1.pcap
    *   [ping](arp1.pcap)

## ARP dans un réseau local

☀️ Déterminer
*  l'adresse IP : 172.20.10.3
* MAC : C8-94-02-F8-AB-97

☀️ DIY
* changer l'adresse IP
```
IPv4 Address. . . . . . . . . . . : 172.20.10.5
```
☀️ Pingz
```
PS C:\WINDOWS\system32> ping 172.20.10.7

Pinging 172.20.10.7 with 32 bytes of data:
Reply from 172.20.10.7: bytes=32 time=41ms TTL=128
Reply from 172.20.10.7: bytes=32 time=31ms TTL=128
Reply from 172.20.10.7: bytes=32 time=36ms TTL=128
Reply from 172.20.10.7: bytes=32 time=23ms TTL=128

Ping statistics for 172.20.10.7:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 23ms, Maximum = 41ms, Average = 32ms
```
## ARP

☀️ Affichez votre table ARP 
* [png](png.pcap)

☀️ Capture arp2.pcap
* [ping](arp2.pcap)


