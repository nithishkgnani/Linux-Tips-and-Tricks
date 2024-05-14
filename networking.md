[Back to Readme](README.md)

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

### Netronome SmartNIC problem

Desciption - Netronome has some issues with handling arp packets. So, we set ARP cache timeout to zero and set the destination mac address here.

```bash
sudo sysctl net.ipv4.neigh.enp1s0f1.gc_stale_time=0
sudo arp -s 10.0.0.1 00:1b:21:c2:54:40
```

## Netem

Netem is a network emulator that can be used to simulate network conditions like latency, packet loss, etc.

* To add a mean delay of 16ms with 4ms normal distribution to the network interface enp3s0  
`sudo tc qdisc add dev enp3s0 root netem delay 16ms 4ms distribution normal`  
* To delete the netem rule  
`sudo tc qdisc del dev enp3s0 root`

## ip and ifconfig

`ip` is the newer command to configure network interfaces. `ifconfig` is the older command.

* To list all network interfaces
`ip a`

* To add an IP address to an interface  
`ip addr add _ipaddr_ dev _interface_`  
Example: `ip addr add 10.0.0.1/24 dev enp3s0`

* To delete an IP address from an interface  
`ip addr del _ipaddr_ dev _interface_`  
Example: `ip addr del 10.0.0.1/24 dev enp3s0`  

    or, Flushing away existing IP address:  
`sudo ip addr flush dev enp3s0`

* To bring an interface up  
`ip link set _interface_ up`

[Back to Readme](README.md)