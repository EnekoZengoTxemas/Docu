---
layout: page
title: Sareak
---


# Sare Planoa

Hasteko aurreko sare planoa hartu genuen. Ondoren aldaketak egin genituen behar genuen guuztia asetu ahal izateko. Sare ia guztia Vlan-etan bihurtu eta swictch-ak jarriz. Horrela geratu zen.

![Placeholder]([https://drive.google.com/file/d/1416pMdMYSkZhPpQH7G_4LUYH60aRW2Vz/view?usp=drive_link](https://drive.google.com/file/d/1LC28lcIU6rHy0pXaMzOxyCz902oIXurJ/view?usp=sharing))

#Packetracer

Ondoren ideia hori packetracer-en muntatu genuen ea funtzionatzen zuen ikusi ahal izateko. Lehendabizi L3 switch-a muntatzen ahisi ginen. 

## - Vlan-ak sortu
  Switch-ean sartu eta bisualki Vlan-etarako interfazea sortu genituen.
   1. Vlan10=SISTEMAK(DHCP)
   2. Vlan20=LANGILEAK(DHCP)
   3. Vlan30=BITARTEKARIA
   4. Vlan40=SISTEMAK
   5. Vlan60=OT

## - IP-ak ezarri
Horretarako urrengo komandoak erabili genituen 
1. interface vlan 10<br>
 ip address 10.1.10.1 255.255.255.0

2. interface vlan 20
   ipv6 enable<br>
   ipv6 address 2600:1700:45c0:e210::/64<br>
   no shutdown<br>

4. interface vlan 30<br>
 ip address 192.168.30.2 255.255.255.0

5. interface vlan 40<br>
 ip address 192.168.40.1 255.255.255.0

6. interface vlan 60<br>
 ip address 192.168.60.1 255.255.255.

## - DHCP
  Ondoren DHCP-a konfiguratu genuen Vlan 10 eta 20 rako<br><br>
      -Vlan10<br>
      ip dhcp pool vlan10<br>
ip dhcp excluded-address 192.168.10.1 192.168.10.10<br>
p dhcp excluded-address 192.168.10.254<br>
network 192.168.10.0 255.255.255.0<br>
default-router 192.168.10.1<br>
exit<br><br>
-Vlan20<br>
ipv6 dhcp pool dhcpipv6<br>
address prefix 2600:1700:45c0:e210::/64<br>
dns-server 2001:4860:4860::8888<br>
exit<br>

##VTP
VTP egin ahal izateko beharrezko portuak trunk-ena jarri ditugu. Ondoren Swich printzipalean hurrengo kodeak jarri ditugu:<br>
vtp domain MiRedLocal <br>
vtp mode server<br>
<br>
Ondoren beste switch-etan klienteak izango direnak urrengoa sartu dugu:<br>
vtp domain MiRedLocal <br>
vtp mode client<br>

