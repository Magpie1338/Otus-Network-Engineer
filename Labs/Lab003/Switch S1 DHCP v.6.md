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
interface range G1/0-3
shutdown
exit
interface g1/2
no shutdown
interface g0/2
no shutdown
interface g0/3
no shutdown
end
copy running-config startup-config
</pre>