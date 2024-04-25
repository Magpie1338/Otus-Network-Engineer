
<pre>
hostname R1
no ip domain-lookup
banner motd #
*********************************
Предупреждение: Несанкционированный доступ  запрещен!
*********************************
#
interface g0/1.100
description Default gateway for VLAN 100
encapsulation dot1Q 100
ip add 192.168.1.1 255.255.255.192
no shutdown

</pre>   
