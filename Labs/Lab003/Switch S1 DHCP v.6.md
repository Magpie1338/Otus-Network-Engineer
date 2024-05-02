<pre>
enable
configure terminal
hostname S1
no ip domain-lookup
banner motd #
*********************************
Attention! Unauthorized access is prohibited!
*********************************
#
interface range G0/0-3
shutdown
exit
interface range G1/0-1
shutdown
exit
vlan 100
name Clients
exit
vlan 200
name Management
exit
vlan 999
name Parking_Lot
exit
interface vlan 200
ip address 192.168.1.66 255.255.255.224
ip default-gateway 192.168.1.65
exit
interface range G0/0-2
switchport mode access
switchport access vlan 999
exit
interface range G1/0-1
switchport mode access
switchport access vlan 999
exit
interface  G1/3
switchport mode access
switchport access vlan 999
exit
interface  G0/3
no shutdown
switchport mode access
switchport access vlan 100
exit
interface  G1/2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk native vlan 1000
switchport trunk allowed vlan 100,200,1000
exit



</pre>