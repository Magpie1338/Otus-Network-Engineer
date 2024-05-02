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
interface range G1/0-3
shutdown
exit
interface g1/2
no shutdown
interface g0/3
no shutdown
exit







</pre>