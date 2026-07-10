11-02-2025 11:39

Status:

Tags: 


# Network Layer 

#### [[Routing]]:
- Routing describes how packets move between different subnets
- Occurs at the Internet Layer
- Occurs when there is a change in IP address space
- Each host has routing table

#### Netmasks:
- Specifies how many bits identify the network prefix
	- e.g. 2001:630:d0::/48
		- The first 48-bits are common to the network
	- e.g. 152.78.0.0/16
		- The first 16 bits are common to the network
		- Can also be represented as 255.255.0.0
- Addresses that fall outside of the netmask for the current networks are in a different IP address space
	- Talking to them requires a router

#### ICMP:
- Internet Control Message Protocol (ICMP)
- ICMP packets are encapsulated in standard IP packets
- IPv4: Used for information and error messages
- IPv6: Also used for Router advertisement and neighbour discovery

#### Multicast:
- One-to-many communication
- Packets are only sent to hosts that are interested in them
- An afterthought for IPv4, inherently required for IPv6
- ff00::/8 for IPv6, 244.0.0.0/4 for IPv4

#### Multicast Uses:
- One-to-many multimedia, e.g. live video streaming
- Local service discovery
	- Multicast DNS allows name resolution in a local network
- Inherently part of IPv6 for router advertisements, neighbour discovery and duplicate address detection

#### ARP:
- Address Resolution Protocol (ARP) maps an IPv4 address on the local subnet to a MAC address
- The host looking for a MAC address broadcasts an ARP "who has" request
- The target sends a (unicast) reply to the requestor
- Each host maintains a local arp cache - view yours with "arp -a"

#### DHCP (IPv4):
- Manually configuring addresses on a network is not the best idea
- Dynamic Host Configuration Protocol (DHCP) automates the process for IPv4
	- When a host connects to a network, it broadcasts a DHCP DISCOVER message
	- The DHCP server reserves an address and replies with DHCP OFFER
	- The client then needs to DHCP REQUEST the address
	- Finally the server sends DHCP ACK, which contains lease duration and config.

#### Neighbour Discovery Protocol (NDP):
- (Technically a link layer thing)
- Maps an IPv6 address on the local subnet to a MAC address
- Uses ICMP and multicast, rather than encapsulated frames and broadcast 
- Router solicitations sent to a solicited node address
- Router advertisements sent to the all nodes address

#### Neighbour Discovery:
- Functionally replaces ARP and ICMP Router Discovery
- Defines five ICMPv6 packet types:
	- Router Solicitation: Host request for router information
	- Router Advertisement: Router information
	- Neighbour Solicitation: Equivalent to ARP "who has"
	- Neighbour Solicitation: Equivalent to ARP "reply"
	- Redirect: Router information host of a "better" first-hop

#### Router Advertisements:
- A host sees or solicits a Router Advertisement (RA):
	- The RA message carries the IPv6 network prefix (/64) to use
	- The RA's source address implies the default router address
	- Flags indicate how addresses are allocated (i.e. SLAAC or DHCP)
	- DNS server can be included in a RA
		- Prefix information is sent by multicast:
			- Periodically (typically every 600 seconds)
			- On request (in response to a Router Solicitation)

#### StateLess Address AutoConfiguration (SLAAC):
- SLAAC allows a host to autoconfigure basic network settings without a DHCPv6 server
- The RA specifies whether SLAAC should be used or not
- A host using SLAAC builds its address from:
	- A 64-bit prefix determined from a Router Advertisement
	- A 64-bit generated host part

#### The RFC4862 Method:
- Host part was originally generated based on a host's MAC address
- For example:
	- Host's Ethernet (MAC) address is 08:00:20:9c:14:66
	- The network prefix in the RA is 2001:630:80:200::/64.
- The RFC4862 address is: 2001:630:80:200:0a00:20ff:fe9c:1466
	- A MAC address is 48 bits, hence the "fffe" 16-bit padding 
	- The "0a" is the globally unique EUI-64 bit being set

#### The RFC7217 Method:
- Embedded the MAC address in a global address is a privacy method nightmare
	- You could track a host across subnets, ISPs, etc. etc.
- But there is a need for a stable IPv6 address for each subnet
- Enter RFC7217 : uses a pseudo-random function that takes the prefix, Network card identifier. Network Identifier, DAD counter and a secret key as arguments 
- The result is a unique but stable address for each subnet that does not embed the MAC address

#### Privacy Extensions:
- A per-subnet stable address can still have privacy implications 
- IPv6 Privacy Extensions (RFC2941) use an ephemeral, randomly-generated host part for outbound connections:
	- Random IPv6 generated periodically (e.g. hourly or daily) and used for outbound connections
	- Address is expired after a period and replaced for outbound connections
	- Old addresses are retained for a period
	- Host still has SLAAC-configured address for inbound connections

#### Privacy Extensions Example:
![[Pasted image 20250310143041.png]]
-  A host will have multiple temporary addresses
- Expired addresses are retained for a while

#### DHCPv6 (RFC8415):
- Similar to DCCP but:
	- Requires Router Advertisement 
	- Uses DHCP Unique Identifier instead of MAC address
	- Terminology:
		- Solicit instead of DISCOVER
		- Advertise instead of OFFER
		- Reply instead of ACK
- Yes, you can have SLAAC and DHCPv6 addresses at the same time
- Can be used just to give extra information (NTP, DNS servers etc.)

	 ![[Pasted image 20250310143823.png]]

#### DHCPv6-PD:
- DHCPv6 can be used to delegate prefixes rather than just single addresses
- This is host most fixed-line ISPs delegate users a nice big block of addresses
- Achieved by specifying an option during the DHCPv6 process
- Once a prefix is delegated, routes need to be updated and a client can distribute the prefix in their network

#### Benefits of Ipv6:
 - Removes the need for NAT:
	 - Restores end-to-end connectivity
	 - Removes the need for NAT traversal
- More plug-and-play than IPv4:
	- Stateless auto configuration (SLAAC) works
- Streamlined header:
	- More efficient routing and packet processing 
- Fragmentation only occurs at sender:
	- Hosts should use Path MTU Discovery (RFC8201)
	- Links must support an MTU of at least 1280
	- Simpler for routers

#### Reasons to deploy now:
- IPv4 is on its last legs
- IPv6 is mandatory
	- Some ISPs ONLY give out IPv6
	- Some sites/services are only available on IPv6
- Enables innovation/teaching/research
- Supports new applications: e.g. IoT
- Allows people to access your services

#### Barriers to Deployment:
- Time and Money:
	- Convincing management that the investment needed is hard
	- Network admins lack understand of IPv6and don't have time
- Hardware support
	- Many older home routers lack IPv6 support
- Regular users don't want to learn something new 
- Chicken and egg situation with ISPs and content providers
- Peering wars between Tier-1 network providers

#### Address Accountability
- IPv6 hosts can essentially pick their own addresses
	- May use many privacy addresses over time 
- To track which devices are used where, we can poll switches and routers for MAC table and ARP table information 
	- Build a database of mappings
	- Switch port - device MAC
	- MAC address - IPv4/IPv6 address
- In ECS, an open source network monitoring package called NAV used to be used for this...


#### IPv6 Myths 
- We don’t need IPv6, CGNAT and address recovery means we have a lot more addresses:
	- NAT and CGNAT only go so far. We already have IPv6-only services. 
- IPv6 replaces IPv4: 
	- Pv6 and IPv4 will co-exist for years to come. 
- IPv6 is more complicated than IPv4: 
	- Addresses look daunting but the concepts are similar or simpler. 
- IPv6 is less secure because there is no NAT: 
	- NAT is NOT a security mechanism and IPv6 still has firewalling/ACLs





# References