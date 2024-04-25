
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


</pre>   
