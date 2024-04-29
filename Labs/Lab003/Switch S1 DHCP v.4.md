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
interface range G0/0-1
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
exit
interface vlan 1
ip address 192.68.1.98 255.255.255.240


</pre>