<pre>
enable
configure terminal
hostname S4
no ip domain-lookup
banner motd #
*********************************
Attention! Unauthorized access is prohibited!
*********************************
#
vlan 10
name Clients
exit
vlan 20
name Clients2
exit
vlan 40
name MNG
exit
vlan 999
name Parking_Lot
exit
spanning-tree mode rapid-pvst
interface range Gi0/3,Gi1/0-3
description Unused ports
shutdown
switchport mode access
switchport access vlan 999
exit
interface Gi0/0
description VPC8
no shutdown
switchport mode access
switchport access vlan 20
exit
interface Gi0/1
description Trunk to S1
no shutdown
switchport trunk encapsulation dot1q
switchport mode trunk
switchport nonegotiate
switchport trunk allowed vlan 10,20,40
exit
interface Gi0/2
description Trunk to S3
no shutdown
switchport trunk encapsulation dot1q
switchport mode trunk
switchport nonegotiate
switchport trunk allowed vlan 10,20,40
exit
interface vlan 40
description Management
ip address 192.168.40.14 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.40.1
end
copy running-config startup-config
</pre>