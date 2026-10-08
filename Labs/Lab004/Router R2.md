<pre>
enable
configure terminal
hostname R2
no ip domain-lookup
banner motd #
*********************************
Attention! Unauthorized access is prohibited!
*********************************
#
interface G0/0
description WAN to R1
ip address 100.0.0.2 255.255.255.0
no shutdown
exit
interface G0/1
description Trunk to S2
no ip address
no shutdown
exit
interface G0/1.10
description VLAN 10 Clients (PC-B)
encapsulation dot1Q 10
ip address 192.168.110.1 255.255.255.0
exit
interface G0/1.40
description VLAN 40 MNG (S2)
encapsulation dot1Q 40
ip address 192.168.140.1 255.255.255.0
exit
ip route 192.168.10.0 255.255.255.0 100.0.0.1
ip route 192.168.20.0 255.255.255.0 100.0.0.1
ip route 192.168.40.0 255.255.255.0 100.0.0.1
ip routing
end
copy running-config startup-config
</pre>