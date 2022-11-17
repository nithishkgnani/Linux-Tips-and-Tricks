_**Warning:**_ Do not try any of these unless you know what exactly you intend to do. Trying some of these commands and tricks may lead to security risks.

## ARP

### manipulating ARP timeout  
* To see what your current ARP timeout is (default is 60 seconds)  
`cat /proc/sys/net/ipv4/neigh/ethX/gc_stale_time`  
* To change the ARP timeout  
`echo _timeout_ > /proc/sys/net/ipv4/neigh/_ethX_/gc_stale_time`  
Here _timeout_ is the new value (in seconds)of ARP timeout. Change the _ethX_ to your interface's name.  
[_Source_](https://serverfault.com/a/684381)

### Static ARP table entries
To avoid arp requests packets from being sent, you can manually add an arp entry:  
* `arp -s _ipaddr_ _macaddr_`  
change the _ipaddr_ and _macaddr_ to the destinations IP address and MAC address.  
[_Source_](https://www.oreilly.com/library/view/network-security-hacks/0596006438/ch03s03.html)