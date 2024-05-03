
<pre>
enable
configure terminal
hostname R1
no ip domain-lookup
banner motd #
*********************************
Attention! Unauthorized access is prohibited!
*********************************
#
ipv6 unicast-routing
interface g0/0
ipv6 address 2001:db8:acad:2::/64 eui-64
no shutdown
interface g0/1
ipv6 address 2001:db8:acad:1::1/64 eui-64
no shutdown




interface g0/0
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
interface g0/1.100
no shutdown
exit
interface g0/1.100
description Default gateway for VLAN 100
encapsulation dot1Q 100
ip address 192.168.1.1 255.255.255.192
no shutdown
exit
interface g0/1.200
description Default gateway for VLAN 200
encapsulation dot1Q 200
ip address 192.168.1.65 255.255.255.224
no shutdown
exit
ip route 192.168.1.96 255.255.255.240 10.0.0.2
ip dhcp excluded-address 192.168.1.0 192.168.1.5
ip dhcp pool CLIENTS-POOL
network 192.168.1.0 255.255.255.192
default-router 192.168.1.1
domain-name ccna-lab.com
lease 2 12 30
ip dhcp excluded-address 192.168.1.96 192.168.1.101
ip dhcp pool R2_Client_LAN
network 192.168.1.96 255.255.255.240
default-router 192.168.1.97
domain-name ccna-lab.com
lease 2 12 30




</pre>   
