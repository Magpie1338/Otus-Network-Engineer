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
spanning-tree vlan 1,10,20,40,999 root secondary
interface range Gi1/0-3
description Unused ports
shutdown
switchport mode access
switchport access vlan 999
exit
interface Gi0/0
description VPC7
no shutdown
switchport mode access
switchport access vlan 10
exit
interface Gi0/1
description Trunk to S4
no shutdown
switchport trunk encapsulation dot1q
switchport mode trunk
switchport nonegotiate
switchport trunk allowed vlan 10,20,40
exit
interface range Gi0/2-3
description EtherChannel to S3
shutdown
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,40
channel-group 1 mode active
exit
interface Port-channel 1
description EtherChannel to S3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport nonegotiate
switchport trunk allowed vlan 10,20,40
exit
interface range Gi0/2-3
no shutdown
exit
interface vlan 40
description Management
ip address 192.168.40.11 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.40.1
end
copy running-config startup-config
</pre>