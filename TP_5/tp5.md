# Setup
➜ Mettre en place le setup suivant :

➜ Ptit tableau avec les adresses IP
```
Nom de la machine
IP dans le LAN 10.5.1.0/24

Votre PC
10.5.1.1

client1.tp5.b1
10.5.1.11

client2.tp5.b1
10.5.1.12

routeur.tp5.b1
10.5.1.254
```
☀️ Uniquement avec des commandes, prouvez-que :

vous avez bien configuré les adresses IP demandées

oyarkin@client1:~/Desktop$ ip a
```powershell
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a3:73:6b brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea3:736b/64 scope link 
       valid_lft forever preferred_lft forever

```

oyarkin@client2:~/Desktop$ ip a
```powershell
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:87:1d:4e brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe87:1d4e/64 scope link 
       valid_lft forever preferred_lft forever

```

routeur :
```powershell
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1d:48:24 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe1d:4824/64 scope link 
       valid_lft forever preferred_lft forever

```
vous avez bien configuré les hostnames demandés
```powershell
oyarkin@client1:~/Desktop$ hostnamectl
 Static hostname: client1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 25d95201e2c24e3bbe983cb99358dbe2
         Boot ID: ac177307372148dbbeabd6a9a5810e7e
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS              
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w
``` 
```powershell
oyarkin@client2:~$ hostnamectl
 Static hostname: client2
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 25d95201e2c24e3bbe983cb99358dbe2
         Boot ID: de9a0b9c12c1441ea7293182df326794
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS              
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w   
```
```powershell
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seg=1 ttl-64 time-56.8 ms
54 bytes from 10.5.1.12: icmp_seg=2 ttl-64 time=2.22 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl-64 time-2.04 ms
64 bytes from 10.5.1.12 : icmp_seq=4 ttl=64 time=2.36 ms
18.5.1. 12 ping statistics
rivéc packets transmitted, 4 received, % packet loss, t ime 5813hns
rtt min/avg/max/mdey = 1.611/11.181/56.800/20.482 s
Lroot@routeur "l# -
```
```powershell
^Cmael@client1:~/Desktop$ ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=8.29 ms
64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=1.28 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=1.38 ms
^C
--- 10.5.1.12 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2010ms
rtt min/avg/max/mdev = 1.284/3.650/8.292/3.282 ms

```

```powershell
oyarkin@client2:~$ ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=1.80 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=1.69 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.894 ms
^C
--- 10.5.1.11 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2015ms
rtt min/avg/max/mdev = 0.894/1.460/1.798/0.402 ms

```

# Accès internet pour tous


## 1. Accès internet routeur

Cette section 1. est à réaliser sur routeur.tp5.b1.

☀️ Déjà, prouvez que le routeur a un accès internet


```powershell
[root@routeur ~]
PING www.ynov.com (184.26.10.233) 56(84) bytes of data.
r ro64 bytes from 184.26.19.233 (184.26.18.233): icmp_seq=1 ttl-54 time -57.4 mS
64 bytes from 194.26.18.233 (184.26.18.233) : icmp_seq=2 ttl-54 time-28.8 ms
64 bytes from 194.26.18.233 (184.26.18.233) : icmp_seq=3 ttl-54 time-18.8 ms
est 64 bytes from 184.26.10.233 (184.26.18.233): icmp_seq=4 ttl-54 time-28.3 ms
^C
Md.ynov.com ping statist ics
4 packets transmitted, 4 received, 0% packet loss, time 3898ms
rtt min/avg/max/mdey = 17.943/29.965/32.435/16.324 ms
```

☀️ Activez le routage


```powershell
[root@routeur ~]
success
[root@routeur ~]
success
[root@routeur ~]
PING www.ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=54 time=18.5 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=54 time=16.9 ms
^C 
--- www.ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 12.558/12.341/18.245/0.793 ms
```
## 2. Accès internet clients

☀️ Prouvez que les clients ont un accès internet


```powershell
oyarkin@client2:~/Desktop$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=53 time=17.5 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=53 time=18.0 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=53 time=21.3 ms
^C
--- ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2010ms
rtt min/avg/max/mdev = 17.467/18.941/21.328/1.703 ms

```

```powershell
oyarkin@client1:~/Desktop$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=53 time=17.7 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=53 time=20.4 ms
64 bytes from 104.26.10.233: icmp_seq=3 ttl=53 time=18.7 ms
^C
--- ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2005ms
rtt min/avg/max/mdev = 17.680/18.917/20.376/1.111 ms

```

☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau

```powershell
oyarkin@client2:~/Desktop$ cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        addresses: [1.1.1.1,1.0.0.1,8.8.8.8]

```

# III. Serveur SSH

☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH


```powershell
[root@routeur ~]
State          Recv-Q         Send-Q         local Adress:Port       Peer Address:Port
LISTEN         0              128            0.0.0.0:22              0.0.0.:*
LISTEN         0              128            [::]:22                 [::]:*
```

☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert

```powershell
[oyarkin@routeur ~]$ sudo firewall-cmd --list-all
[sudo] password for oyarkin:
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

# IV. Serveur DHCP

☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1

```powershell
[oyarkin@routeur ~]$ sudo nano /etc/dhcp/dhcpd.conf

option domain-name "world";

option domain-name-servers 1.1.1.1;

default-lease-time 600;

max-lease-time 7200;

authoritative;

subnet 10.5.1.0 netmask 255.255.255.0 {
    range 10.5.1.137 10.5.1.237;
    
    option broadcast-address 10.5.1.255;
    
    option routers 10.5.1.254;
}


[oyarkin@routeur ~]$ systemctl enable --now dhcpd
Failed to enable unit: Access denied
[oyarkin@routeur ~]$ sudo systemctl enable --now dhcpd
[oyarkin@routeur ~]$ sudo systemctl restart dhcpd
[mael@routeur ~]$ sudo systemctl enable dhcpd

[oyarkin@routeur ~]$
[oyarkin@routeur ~]$ sudo firewall-cmd --add-service=dhcp --permanent
md --reload
Warning: ALREADY_ENABLED: dhcp
success
[oyarkin@routeur ~]$ sudo firewall-cmd --reload
success
[oyarkin@routeur ~]$
```

B. Test avec un nouveau client

☀️ Créez une nouvelle machine client client3.tp5.b1

```powershell
oyarkin@oyarkin-VirtualBox:~/Desktop$ hostnamectl
 Static hostname: client3
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 25d95201e2c24e3bbe983cb99358dbe2
         Boot ID: 667803396c354428a51c0e734e2a16e9
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS              
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w 1d   
oyarkin@oyarkin-VirtualBox:~/Desktop$ sudo nano /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: yes
oyarkin@oyarkin-VirtualBox:~/Desktop$ sudo netplan apply

** (generate:6187): WARNING **: 12:17:19.197: Permissions for /etc/netplan/01-netcfg.yaml are too open. Netplan configuration should NOT be accessible by others.

** (process:6186): WARNING **: 12:17:19.475: Permissions for /etc/netplan/01-netcfg.yaml are too open. Netplan configuration should NOT be accessible by others.

** (process:6186): WARNING **: 12:17:19.566: Permissions for /etc/netplan/01-netcfg.yaml are too open. Netplan configuration should NOT be accessible by others.
oyarkin@oyarkin-VirtualBox:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:0e:b4:ef brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 metric 100 brd 10.5.1.255 scope global dynamic enp0s8
       valid_lft 561sec preferred_lft 561sec
oyarkin@oyarkin-VirtualBox:~/Desktop$ ping www.ynov.com
PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=53 time=18.3 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=53 time=21.3 ms
64 bytes from 104.26.10.233: icmp_seq=3 ttl=53 time=19.2 ms
^C
--- www.ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2018ms
rtt min/avg/max/mdev = 21.322/14.439/23.443/1.265 ms

```

C. Consulter le bail DHCP

☀️ Consultez le bail DHCP qui a été créé pour notre client

```powershell
[oyarkin@routeur dhcpd]$ sudo cat dhcpd.leases

authoring-byte-order little-endian;

server-duid "\000\001\000\001.\242FB\010\000'\3725\272";

lease 10.5.1.134 {
  starts 3 2024/10/16 10:12:39;
  ends 3 2024/10/16 10:22:39;
  cltt 3 2024/10/16 10:12:39;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:0e:b4:ef;
  uid "\377\3424?>\000\002\000\000\253\021a\201\251\252\350\277\325\012";
  client-hostname "client3";
}
lease 10.5.1.134 {
  starts 3 2024/10/16 10:12:39;
  ends 3 2024/10/16 10:17:21;
  tstp 3 2024/10/16 10:17:21;
  cltt 3 2024/10/16 10:12:39;
  binding state free;
  hardware ethernet 08:00:27:0e:b4:ef;
  uid "\377\3424?>\000\002\000\000\253\021a\201\251\252\350\277\325\012";
}
lease 10.5.1.134 {
  starts 3 2024/10/16 10:17:25;
  ends 3 2024/10/16 10:27:25;
  cltt 3 2024/10/16 10:17:25;
  binding state active;
  next binding state free;
  rewind binding state free;
  ☀️hardware ethernet 08:00:27:0e:b4:ef;
  uid "\377\3424?>\000\002\000\000\253\021a\201\251\252\350\277\325\012";
  client-hostname "client3";
}
```

☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC

```powershell
oyarkin@oyarkin-VirtualBox:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    ☀️link/ether 08:00:27:0e:b4:ef brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 metric 100 brd 10.5.1.255 scope global dynamic enp0s8
       valid_lft 498sec preferred_lft 498sec

```