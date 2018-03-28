# Packet Capture (pcap) tools

* Record a packet capture with [tcpdump](#tcpdump)
* Modify a packet capture with [tcprewrite](#tcprewrite)
* Transmit a packet capture with [tcpreplay](#tcpreplay)
* Record a packet capture with [tshark](#tshark)

## tcpdump
```
sudo tcpdump -w output.pcap -i eth0 -Z username udp port 60000
```
|Argument|Note|
|-|-|
|sudo|typically tcpdump requires elevated permissions|
|-w output.pcap|writes to the provided filename|
|-i eth0|specifies the interface|
|-Z username|sets owner of the output file to username (useful if running with sudo)|
|udp port 60000|packet filter string (in the example, only capture udp packets matching port 60000)|

#### Notes:
* [External documentation](https://www.tcpdump.org/tcpdump_man.html)
* Double-check to make sure the interface and port are correct
* if recording multicasts, make sure to start an active multicast receiver that will send the proper IGMP join (tcpdump does not do this)

## tcprewrite
```
tcprewrite -i orginal.pcap -o new.pcap -S 1.2.3.4:1.2.3.5 -D 1.2.3.6:1.2.3.7 --portmap=5001:6001 --enet-smac=00:01:02:03:04:05 --enet-dmac=0A:0B:0C:0D:0E:0F -C --enet-vlan=del
```
|Argument|Note|
|-|-|
|-i orginal.pcap|specifies the input file|
|-o new.pcap|rewrites to the provided filename|
|-S 1.2.3.4:1.2.3.5|modifies the source IP address (format is old:new)|
|-D 1.2.3.6:1.2.3.7|modifies the destination IP address (format is old:new)|
|--portmap=5001:6001|modifies the src or dst port number (format is old:new)|
|--enet-smac=00:01:02:03:04:05|sets a new source mac address|
|--enet-dmac=0A:0B:0C:0D:0E:0F|sets a new destination mac address|
|-C|recalculates protocol checksums|
|--enet-vlan=del|sets a new VLAN ID or removes the VLAN tag|

#### Notes:
* [External documentation](http://tcpreplay.synfin.net/wiki/tcprewrite)
* Changing addresses/ports typically requires the checksum recalculation otherwise protocol layers will reject packets
* if destination IP is a multicast the destination mac address will need to match.  Use a  [calculator](https://www.google.com/search?q=ethernet+multicast+calculator)
* may have to remove the VLAN ID to get a replay to work in a different environment

## tcpreplay
```
sudo tcpreplay -i eth0 -p 10 --loop=5 replay.pcap
```
|Argument|Note|
|-|-|
|sudo|typically tcpreplay requires elevated permissions|
|-i eth0|specifies the interface|
|-p 10|specifies the number of packets per second to send|
|--loop=5|specifies how many times to replay the entire file (0 is infinite)|
|replay.pcap|the filename to replay|

#### Notes:
* [External documentation](http://tcpreplay.synfin.net/wiki/tcpreplay)
* Double-check to make sure interface is correct

## tshark
```
tshark -w output.pcap -i eth0 udp port 60000
```
|Argument|Note|
|-|-|
|-w output.pcap|writes to the provided filename|
|-i eth0|specifies the interface|
|udp port 60000|packet filter string (in the example, only capture udp packets matching port 60000)|
