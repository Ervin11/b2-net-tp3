
# TP3 - Utilisation de matériel Cisco
---  

#### I. Manipulation de switches et de VLAN

##### 1. Mise en place du lab  

&nbsp;

***Test de ping***

```sh
# Client 1
[ervin@client1 ~]$ ping -c 2 client2
64 bytes from client2.lab1.tp3 (10.1.1.2): icmp_seq=1 ttl=64 time=10.2 ms
64 bytes from client2.lab1.tp3 (10.1.1.2): icmp_seq=2 ttl=64 time=3.91 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

[ervin@client1 ~]$ ping -c 2 client3
64 bytes from client3.lab1.tp3 (10.1.1.3): icmp_seq=1 ttl=64 time=8.49 ms
64 bytes from client3.lab1.tp3 (10.1.1.3): icmp_seq=2 ttl=64 time=1.89 ms
2 packets transmitted, 2 received, 0% packet loss, time 1001ms

# Client 2
[ervin@client2 ~]$ ping -c 2 client1
64 bytes from client1.lab1.tp3 (10.1.1.1): icmp_seq=1 ttl=64 time=1.56 ms
64 bytes from client1.lab1.tp3 (10.1.1.1): icmp_seq=2 ttl=64 time=2.01 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

[ervin@client2 ~]$ ping -c 2 client3
64 bytes from client3.lab1.tp3 (10.1.1.3): icmp_seq=1 ttl=64 time=6.75 ms
64 bytes from client3.lab1.tp3 (10.1.1.3): icmp_seq=2 ttl=64 time=1.75 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

# Client 3
[ervin@client3 ~]$ ping -c 2 client1
64 bytes from client1.lab1.tp3 (10.1.1.1): icmp_seq=1 ttl=64 time=2.04 ms
64 bytes from client1.lab1.tp3 (10.1.1.1): icmp_seq=2 ttl=64 time=1.62 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

[ervin@client3 ~]$ ping -c 2 client2
64 bytes from client2.lab1.tp3 (10.1.1.2): icmp_seq=1 ttl=64 time=1.97 ms
64 bytes from client2.lab1.tp3 (10.1.1.2): icmp_seq=2 ttl=64 time=1.78 ms
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
```

##### 2. Configuration des VLANs
&nbsp;
```sh
#Switch 1

IOU1#show vlan br

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   client1                          active    Et0/0
20   client2                          active    Et0/1
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 

# Switch 2

IOU2#show vlan br

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/2, Et0/3, Et1/0, Et1/1
                                                Et1/2, Et1/3, Et2/0, Et2/1
                                                Et2/2, Et2/3, Et3/0, Et3/1
                                                Et3/2, Et3/3
10   client3                          active    Et0/1
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 
```

***Test Ping***

```sh
# Client 1
[ervin@client1 ~]$ ping -c 2 client3
64 bytes from client3.lab1.tp3 (10.1.1.3): icmp_seq=1 ttl=64 time=3.88 ms
64 bytes from client3.lab1.tp3 (10.1.1.3): icmp_seq=2 ttl=64 time=27.5 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

# Client 3
[ervin@client3 ~]$ ping -c 2 client1
64 bytes from client1.lab1.tp3 (10.1.1.1): icmp_seq=1 ttl=64 time=9.89 ms
64 bytes from client1.lab1.tp3 (10.1.1.1): icmp_seq=2 ttl=64 time=19.1 ms
2 packets transmitted, 2 received, 0% packet loss, time 1003ms

# Client 2 injoignable

[ervin@client1 ~]$ ping -c 2 client2
2 packets transmitted, 0 received, 100% packet loss, time 1000ms

[ervin@client3 ~]$ ping -c 2 client2
2 packets transmitted, 0 received, 100% packet loss, time 1002ms
```

#### II. Manipulation simple de routeurs
##### 1. Mise en place du lab
&nbsp;
```sh
# Client 1 n'a pas de gateway
# Client 2 vers sa gateway
[ervin@client2 ~]$ ping -c 2 10.2.10.254
64 bytes from 10.2.10.254: icmp_seq=1 ttl=64 time=21.8 ms
64 bytes from 10.2.10.254: icmp_seq=2 ttl=64 time=11.3 ms
2 packets transmitted, 2 received, 0% packet loss, time 1001ms

# Server 1 vers sa gateway
[ervin@server1 ~]$ ping -c 2 10.2.2.254
64 bytes from 10.2.2.254: icmp_seq=1 ttl=64 time=20.9 ms
64 bytes from 10.2.2.254: icmp_seq=2 ttl=64 time=2.71 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

# Router 1 vers Router 2
R1# ping 10.2.12.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.2.12.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 12/24/56 ms

# Router 2 vers Router 1
R2# ping 10.2.12.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.2.12.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/49/72 ms
```

##### 2. Configuration du routage statique
&nbsp;
```sh
# Client 1 n'a pas de gateway donc le routage est inutile, il ne peut joindre personne.
# Client 2 vers Server 1 en passant par Router 1 et Router 2
[ervin@server1 ~]$ ping -c 2 10.2.2.10
64 bytes from 10.2.2.10: icmp_seq=1 ttl=64 time=26.2 ms
64 bytes from 10.2.2.10: icmp_seq=2 ttl=64 time=43.3 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

# Server 1 vers Client 2 en passant par Router 1 et Router 2
[ervin@server1 ~]$ ping -c 2 10.2.2.10
64 bytes from 10.2.2.10: icmp_seq=1 ttl=64 time=26.2 ms
64 bytes from 10.2.2.10: icmp_seq=2 ttl=64 time=43.3 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
```

**Proposition de topologie :**  

Il suffirait d'ajouter et configurer un switch dans le réseau 10.2.1.0/24, auquel Client 1 et Client 2 seraient connectés et le switch serait relié au Router 1 qui lui même est relié au Router 2 et ce dernier au Server 1.

#### III. Mise en place d'OSPF
##### 1. Mise en place du lab
&nbsp;

```sh
# Client 1 vers sa gateway
[ervin@client1 ~]$ ping -c 2 10.3.101.254
PING 10.3.101.254 (10.3.101.254) 56(84) bytes of data.
64 bytes from 10.3.101.254: icmp_seq=1 ttl=255 time=8.46 ms
64 bytes from 10.3.101.254: icmp_seq=2 ttl=255 time=6.69 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

# Server 1 vers sa gateway
[ervin@server1 ~]$ ping -c 2 10.3.102.254
PING 10.3.102.254 (10.3.102.254) 56(84) bytes of data.
64 bytes from 10.3.102.254: icmp_seq=1 ttl=255 time=23.4 ms
64 bytes from 10.3.102.254: icmp_seq=2 ttl=255 time=4.67 ms
2 packets transmitted, 2 received, 0% packet loss, time 1002ms

# Router 1 vers Router 2
R1#ping 10.3.100.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.100.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 64/65/68 ms

# Router 4 vers Router 5
R4#ping 10.3.100.14

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.100.14, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 12/44/68 ms
```
#### 2. Configuration de OSPF
&nbsp;

```sh
# Tous les routeurs peuvent se joindre

R1#traceroute 10.3.100.10 (IP Router 4 : passe par Router 2 et Router 3)

Tracing the route to 10.3.100.10

  1 10.3.100.2 16 msec 8 msec 12 msec
  2 10.3.100.6 24 msec 24 msec 16 msec
  3 10.3.100.10 32 msec 36 msec 44 msec
  
R1#traceroute 10.3.100.13 (IP Router 4 : passe par Router 6 et Router 5)

Tracing the route to 10.3.100.13

  1 10.3.100.21 36 msec 24 msec 0 msec
  2 10.3.100.17 16 msec 20 msec 28 msec
  3 10.3.100.13 20 msec 36 msec 60 msec
  
# Client 1 ping Server 1 et vice versa

[ervin@client1 ~]$ ping -c 2 10.3.102.10
PING 10.3.102.10 (10.3.102.10) 56(84) bytes of data.
64 bytes from 10.3.102.10: icmp_seq=1 ttl=60 time=63.0 ms
64 bytes from 10.3.102.10: icmp_seq=2 ttl=60 time=54.7 ms

2 packets transmitted, 2 received, 0% packet loss, time 1000ms
```

Traceroute ne fonctionne pas entre Client 1 et Server 1, je n'ai pas réussi à trouver le bug.

#### IV. Lab Final

**Client 1** : 10.10.1.1 / 255.255.255.0 / Vlan 10  
**Client 2** : 10.20.1.1 / 255.255.255.0 / Vlan 20  
**Server 1** : 10.10.1.2 / 255.255.255.0 / Vlan 10

```sh
# Configuration VLAN Switch 1

IOU1#show vlan br
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et1/0, Et1/1, Et1/2, Et1/3
                                                Et2/0, Et2/1, Et2/2, Et2/3
                                                Et3/0, Et3/1, Et3/2, Et3/3
10   client1                          active    Et0/0
20   client2                          active    Et0/1
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 

# Test de ping de Client 1 à Client 2

[ervin@client1]# ping 10.20.1.1
PING 10.20.1.1 (10.20.1.1) 56(84) bytes of data.
From 10.10.1.1 icmp_seq=1 Destination Host Unreachable
From 10.10.1.1 icmp_seq=2 Destination Host Unreachable
From 10.10.1.1 icmp_seq=3 Destination Host Unreachable
From 10.10.1.1 icmp_seq=4 Destination Host Unreachable

4 packets transmitted, 0 received, +3 errors, 100% packet loss, time 8007ms

# Configuration VLAN Switch 2

IOU2#show vlan br
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/2, Et0/3, Et1/0, Et1/1
                                                Et1/2, Et1/3, Et2/0, Et2/1
                                                Et2/2, Et2/3, Et3/0, Et3/1
                                                Et3/2, Et3/3
10   server1                          active    Et0/0
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 

# Test de ping Client 1 à Server 1

[ervin@client1]# ping -c 2 10.10.1.2
PING 10.10.1.2 (10.10.1.2) 56(84) bytes of data.
64 bytes from 10.10.1.2: icmp_seq=1 ttl=64 time=22.7 ms
64 bytes from 10.10.1.2: icmp_seq=2 ttl=64 time=4.25 ms

2 packets transmitted, 2 received, 0% packet loss, time 1002ms
```

**Mise en place de l'inter VLAN**

```sh
# Mise en place de 2 sous-interfaces sur Routeur 1 : VLAN 10 et VLAN 20

R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  up                    up      
FastEthernet0/0.1          10.10.1.254     YES manual up                    up      
FastEthernet0/0.2          10.20.1.254     YES manual up                    up      
FastEthernet1/0            unassigned      YES unset  administratively down down    
FastEthernet2/0            unassigned      YES unset  administratively down down    
FastEthernet3/0            unassigned      YES unset  administratively down down

# Test de ping entre Client 1 et Client 2

[ervin@client1 ~]$ ping -c 2 10.20.1.1
PING 10.20.1.1 (10.20.1.1) 56(84) bytes of data.
64 bytes from 10.20.1.1: icmp_seq=1 ttl=63 time=65.8 ms
64 bytes from 10.20.1.1: icmp_seq=2 ttl=63 time=74.1 ms

2 packets transmitted, 2 received, 0% packet loss, time 1001ms
```
**Mise en place d' OSPF**

```sh
# Test OSPF : Traceroute de Routeur 1 à Routeur 4 en passant par Routeur 2

R1#traceroute 10.100.4.2    
Tracing the route to 10.100.4.2

  1 10.100.1.2 20 msec 28 msec 16 msec
  2 10.100.4.2 24 msec 40 msec 28 msec

# Test OSPF : Traceroute de Routeur 1 à Routeur 4 en passant par Routeur 3

R1#traceroute 10.100.3.2
Tracing the route to 10.100.3.2

  1 10.100.2.2 8 msec 12 msec 20 msec
  2 10.100.3.2 36 msec 36 msec 20 msec

# Test OSPF : Traceroute de Routeur 1 à la passerelle out de Routeur 4 

R1#traceroute 192.168.122.15
Tracing the route to 192.168.122.15

  1 10.100.2.2 16 msec
    10.100.1.2 16 msec
    10.100.2.2 8 msec
  2 10.100.4.2 40 msec
    10.100.3.2 32 msec
    10.100.4.2 24 msec
```

**Mise en place de NAT**

```sh
# Routeur 4
interface FastEthernet0/0
 ip address 10.100.4.2 255.255.255.252
 ip nat inside
         
interface FastEthernet1/0
 ip address 10.100.3.2 255.255.255.252
 ip nat inside
         
interface FastEthernet2/0
 ip address dhcp
 ip nat outside
 
# Test de fonctionnement NAT à partir de Client 1

[ervin@client1]# curl google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>

# Test de fonctionnement NAT à partir de Client 2

[ervin@client2 ~]$ curl google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>

# Test de fonctionnement NAT à partir de Server 1

[ervin@server1 ~]$ curl google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```
**Topologie**

<img src="https://github.com/Ervin11/b2-net-tp3/blob/master/TP3-lab4.png"/>
