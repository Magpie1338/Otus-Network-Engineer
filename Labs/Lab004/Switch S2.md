<pre>
enable
configure terminal
hostname S2
no ip domain-lookup
banner motd #
*********************************
Attention! Unauthorized access is prohibited!
*********************************
#
vlan 10
name Clients
exit
vlan 40
name MNG
exit
vlan 999
name Parking_Lot
exit
spanning-tree mode rapid-pvst
spanning-tree vlan 1,10,40,999 root primary
interface range Gi0/1-3
description Unused ports
shutdown
switchport mode access
switchport access vlan 999
exit
interface range Gi1/0-1,Gi1/3
description Unused ports
shutdown
switchport mode access
switchport access vlan 999
exit
interface Gi0/0
description PC-B
no shutdown
switchport mode access
switchport access vlan 10
exit
interface Gi1/2
description Trunk to R2
no shutdown
switchport trunk encapsulation dot1q
switchport mode trunk
switchport nonegotiate
switchport trunk allowed vlan 10,40
exit
interface vlan 40
description Management
ip address 192.168.140.12 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.140.1
end
copy running-config startup-config
</pre>