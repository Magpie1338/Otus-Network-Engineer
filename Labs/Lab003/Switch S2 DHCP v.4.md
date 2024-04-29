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
interface range G0/0-3
shutdown
exit
interface range G0/0-1
shutdown
exit
interface vlan 1
ip address 192.68.1.98 255.255.255.240
exit






</pre>