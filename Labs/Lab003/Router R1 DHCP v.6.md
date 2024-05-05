
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
ipv6 unicast-routing
interface g0/0
ipv6 address 2001:db8:acad:2::1/64
no shutdown
interface g0/1
ipv6 address 2001:db8:acad:1::1/64
no shutdown
exit
ipv6 route ::/0 2001:db8:acad:2::2
end
copy running-config startup-config
</pre>   
Настройка stateless DHCPv6
<pre>
enable
configure terminal
ipv6 dhcp pool R1-STATELESS
dns-server 2001:db8:acad::254
domain-name STATELESS.com
interface g0/1
ipv6 nd other-config-flag
ipv6 dhcp server R1-STATELESS
end
copy running-config startup-config
</pre>
Настройка stateful DHCPv6
<pre>
enable
configure terminal
ipv6 dhcp pool R2-STATEFUL
address prefix 2001:db8:acad:3:aaa::/80
dns-server 2001:db8:acad::254
domain-name STATEFUL.com
interface g0/0
ipv6 dhcp server R2-STATEFUL
end
copy running-config startup-config
</pre