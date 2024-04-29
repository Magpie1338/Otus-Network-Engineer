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
interface range G0/0-3
shutdown
exit
interface range G0/0-1
shutdown
exit






</pre>