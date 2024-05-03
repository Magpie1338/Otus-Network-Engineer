
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
ipv6 unicast-routing
interface g0/0
ipv6 address 2001:db8:acad:2::2/64 eui-64
no shutdown
interface g0/1
ipv6 address 2001:db8:acad:3::1/64 eui-64
no shutdown



interface G0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit
interface G0/1
ip address 192.168.1.97 255.255.255.240
no shutdown
exit
ip route 192.168.1.0 255.255.255.192 10.0.0.1
ip route 192.168.1.64 255.255.255.224 10.0.0.1
ip helper-address 10.0.0.1


</pre>   
