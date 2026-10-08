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
interface G0/0
description WAN to R2
ip address 100.0.0.1 255.255.255.0
no shutdown
exit
interface G0/1
description Trunk to S3
no ip address
no shutdown
exit
interface G0/1.10
description VLAN 10 Clients (VPC7)
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
interface G0/1.20
description VLAN 20 Clients2 (VPC8)
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
interface G0/1.40
description VLAN 40 MNG (S1, S3, S4)
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0
exit
ip route 192.168.110.0 255.255.255.0 100.0.0.2
ip route 192.168.140.0 255.255.255.0 100.0.0.2
ip routing
end
copy running-config startup-config
</pre>