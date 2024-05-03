
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
ipv6 address 2001:db8:acad:2::2/64
no shutdown
interface g0/1
ipv6 address 2001:db8:acad:3::1/64
no shutdown
exit
ipv6 route ::/0 g0/0
</pre>   
