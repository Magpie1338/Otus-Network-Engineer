
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
ip add 10.0.0.2 255.255.255.252
exit

</pre>   
