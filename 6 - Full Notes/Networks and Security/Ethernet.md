22-04-2025 22:06

Status:

Tags: [[Networks and Security]]


# Ethernet

#### Ethernet Networking:
- Ethernet in its various forms is a core enabling technology for many networks
	- Campus networks
		- Will have lots at high speed e.g. 1 Gbit/s
	- Home networks
		- Mainly wireless for convenience
		- But some Ethernet and powerline Ethernet

#### Ethernet Frame:
- In the [[Link Layer]]
- An Ethernet frame includes:
	- 48-bit source and destination MAC addresses
	- 802.1Q tag for optional VLAN ID and frame priority
- Maximum Transmission Unit/MTU usually 1500 bytes
	- Larger messages are broken down into multiple frames which are then re-assembled by the receiver
	![[Pasted image 20250422221241.png]]

#### MAC Addresses:
- Link layer addresses:
	- Usually referred to as MAC addresses (Medium Access Control)
	- Currently defined to be 48 bits, extensible to 64 bits
- Needs to be unique
	- 24 bits used for vendor allocations
	- Last 24 bits assigned by vendor

#### Building Ethernet networks:
- Each host typically connects to a port on a switch
- Desktops now typically 1 Gbit/s (or 2.5) Ethernet
- Servers and backbone on 10 Gbit/s Ethernet (or 25/50/100)

#### Ethernet Switches:
- Receive Ethernet frames and make a decision whether to forward the frame, and if so, on which port
	- Provides "smart" forwarding 
	- It learns Ethernet MAC addresses of host(s) seen on each switch interface/port
	- Hosts generally only see packets sent to them, or broadcast packets
- Can store and forward Ethernet frames
	- So can check for errors (CRC check) before forwarding
- Some switches support more advanced functions
	- e.g. VLANs, QoS, management...

#### MAC with switches:
- Allows a switch to only forward frames to ports where the devices they are addressed to are connected
- Observes incoming source Ethernet (MAC) addresses on each switch port
	- Stores observed MAC source addresses in the switch port table
- Can then forward future frames sent to that address to that port
	- And to that port only 
	- Broadcast frames are still forwarded everywhere 
	- Hosts only see traffic sent to them, or any broadcast/multicast traffic
	- An important security consideration
	- If the MAC address is not in any table, switch must flood it to all ports
- MAC table entries will time out after a short period (e.g. 60 secs)

#### Sending IP datagrams over Ethernet 
- Link layer receives datagrams from the network (IP) layer
- Encapsulates these as the payload of an Ethernet frame 
- IP datagram has a source and destination IP address
- Need to forward it to the destination IP address using the Ethernet layer
- Implies the network layer can determine the Ethernet address of the destination IP address
	- Need method to "resolve" an IP address to a MAC address
- (This is local LAN not internet)

#### ARP - Address Resolution Protocol
- Used to determine the destination's MAC address
	- RFC 826
- ARP uses a link layer broadcast message
	- To the special Ethernet broadcast address ff:ff:ff:ff:ff:ff
		- Sender asks "Who has this IP address?"
	- Seen by all hosts in the same Ethernet LAN
		- The host with the target IP responds
	- Sender can then use result to send Ethernet frame
		- Caches the result (e.g. 15-45 seconds on Win10)

#### Aside: message types:
- Unicast
	- From one sender to one receiver
- Broadcast
	- From one sender to all potential receivers
	- Some protocols rely on one device being able to send a message seen by all other devices at that network layer
	- Can have link layer and network layer broadcasts, for example:
		- Multicast
			- From one sender to any number of "interested" receivers
		- Anycast
			- From one sender to nearest instance of receiver
#### ARP message format:
![[Pasted image 20250422223940.png]]


#### Nuances of ARP:
- Is it secure?
	- ARP is potentially open to spoofing
		- Pretending to have an IP address
	- Note that a host can change its MAC address
- Change of IP or MAC address
	- Send a "gratuitous ARP"
	- Enables a quick update of the correct information
- ARP probe
	- To detect IP address clashes (is anyone using this address?)

#### LAN Communication:
- NS: neighbour solicitation (IVMPv6 type 135)
- NA: Neighbour advertisement (IVMPv6 type 136)

#### Ethernet Broadcast Domains:
- Even in a switched network, Ethernet broadcasts will flood the LAN
	- In a 20,000 host campus network, that is a lot of broadcasts
	- Wireless APs will also be plugged in
	- And ARP isn't the only protocol that does broadcasts
- Therefore we must keep Ethernet LANs limited to a reasonable size
	- In a campus, typically a LAN per floor or per building

#### Connecting Ethernet LANs
- When we create an Ethernet LAN with switches, all the devices on the LAN can talk directly to each other, using their link layer (MAC addresses)
- A LAN will also use a certain range of [[Network Layer]] IP address
	- e.g. 152.78.10.0 to 152.78.10.255 (256) addresses
- If we wish to connect two such LANs together, we need to use an IP (network layer) router
- The router then forwards the IP packets between the LANs
	- Routers do not forward Ethernet (Link Layer) broadcasts; they handle IP
- The router will typically advertise to other routers the reachability of the IP address range it directly serves.
# References