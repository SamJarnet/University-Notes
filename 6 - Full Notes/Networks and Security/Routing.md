07-02-2025 09:39

Status:

Tags: [[Networks and Security]] 


# Routing

#### Routing:
- A function of the Internet Layer
- Routing describes how packets move between different subnets
- We will be using IPv4 examples for simplicity, but this applies to IPv6 as well

#### Netmasks:
- Specifies how many bits identify the network prefix
	- e.g. 2001:630:d0::/48
		- The first 48-bits are common to the network (remain unchanged)
	- e.g. 152.78.0.0/16
		- The first 16 bits are common to the network
		- Can also be represented as 255.255.0.0
- Addresses that fall outside of the netmask for the current network are in a different IP address space.
	- Talking to them requires the router

#### Basic Routing:
- P1's packet is sent to the nearest router,
- The packet is then passed on through the network,
- Eventually it arrives at P2

#### IP Routing:
- Occurs when there is a change in IP address space
- A router has an IP address in each address space it routes between
- There can be many routers between hosts on the Internet
	- a host can only directly send packets to a router on its own subnet
- Parts of the IP header are re-written at each hop

#### View from a Host
- A host needs to know where to send a packet:
	- Send directly to a destination on the same local subnet
	- Or Forward to a router
- Hosts are (usually) unaware of routes beyond their own subnet
- Hosts may have multiple possible routers

#### Example: A local subnet view:
- Consider a host 152.78.68.162
- Lets say DHCP assigns:
	- default router 152.78.68.190
	- and netmask 255.255.255.192 (/26)
![[Pasted image 20250207095036.png]]

#### Routing Table:
- All hosts on a network have a routing table
- May be built from information from DHCP or IPv6 RA
- For most hosts, this is small and includes:
	- destination IP prefixes and the interface or next hop to use
	- the local subnet that the host is connected to
	- a catchall "default route"
- Tells the host how to route traffic

#### Examples:
![[Pasted image 20250207095324.png]]![[Pasted image 20250207095336.png]]

#### Routing Tables (continued)
- Routing table is a set of rules 
- There can be multiple routes for one destination
- The most specific matching route is picked first
	- e.g. the route with the longest prefix
- The metric determines the priority of routes with the same specificity
	- A lower metric means a higher priority


#### Prefix Aggregation:
- In principle all Internet routers would need to know the presence of every subnet on the Internet
- In practice this is not needed:
	- A subnet's prefix can be aggregated with other adjacent subnets
	- E.g. 192.168.10.0/24 and 192.168.11.0/24 can be aggregated to 192.168.10.0/23
- An organisation might only advertise one route for its entire address space
- N.B. IPv4 exhaustion makes prefix aggregation harder and routing tables larger

#### Beyond the default router:
- We said that IP packets not delivered locally are sent via the default router
- The default router (and any routers beyond it) needs to know where to send the packet next - it has its own routing table
	- This could be VERY large and subject to frequent changes
	- Manual configuration may not be feasible
- This is where routing protocols come in

#### Autonomous Systems:
- An AS is a large network or group of networks that has a unified policy
- The Internet is made of interconnected AS 
- Each AS is assigned an Autonomous System Number (ASN) by a RIR (the same bodies that allocate IPs), e.g. JISC is AS 786
- Three general categories of AS:
	- Multihomed
	- Transit
	- Single-homed/stub

#### Routing Protocols 
- A routing protocol allows router to build and exchange routing information automatically
- Different protocols are used for different networks:
	- Interior gateway protocols are used within an AS
		- e.g. within a corporate network
	- Exterior gateway protocols are used between AS
		- e.g. the internet

#### Types of Interior Gateway Protocol:
- Distance Vector:
	- Talk only to directly neighbouring routers
	- Exchange "best" route (shortest distance) information for any known prefixes with direct neighbours
		- e.g. RIP
- Link state:
	- Talk to all routers to establish full knowledge of the routers/topology of a site
	- Routers flood information messages describing their connected neighbours around entire site network
		- e.g. IS-IS, OSPF

#### RIP:
- Router sends its whole routing table periodically (every 30s) to directly connected routers
	- Destination network (prefix) and distance (cost) in hops
	- Receiving routers update their view of the best route (lowest distance) to a given network (prefix)

#### RIP example:
![[Pasted image 20250207102240.png]]

#### RIP Limitations:
- Updates only sent every 30s
- Updates are not acknowledged (UDP)
- Metrics are simple hop count values 
	- Limited to max value of 15 - a value of 16 means unreachable
- Routers don't have knowledge of network topology 
	- Can lead to "count to infinity" problem
- Authentication is MD5 (RIP 1 and RIP 2), which is broken

#### Link State Routing:
- De facto enterprise routing algorithm
	- Usually IS-IS or OSPF
- Steps:
	- 1. Discover neighbours & determine cost metric
	- 2. Message with this information to all routers
	- 3. Use received messages to build topology: compute shortest paths for prefixes served by aby router
- Messages are sent periodically, or any time a change in connectivity is detected
- Both ends of a link must agree for it to be valid
- All routers learn the full network topology

#### Discovering Neighbours:
- Neighbours are discovered with broadcast packets sent on all interfaces
- Link cost is then determined:
	- Typically based on bandwidth and/or delay 
	- Could be based on other factors

#### Building link state packets:
- Each router creates link states packets based on neighbours and costs to reach them
- The packets are sent to all routers in the network
	- May be multicast or broadcast
	- Sent periodically or when requested

#### Computing shortest path tree:
- Each route computes the best paths 
- Uses Dijkstra's Algorithm to build a tree:
	- Determines shortest path through a graph from an initial node to any given destination
	- Algorithm works by expanding from the starting node, considering cheapest neighbour with each iteration
	- similar algorithm on sat navs
- The tree is then used to populate the routing table

#### Link State vs Distance Vector:
- Link state converges faster:
	- E.g. OSPF can detect changes to topology and converge in seconds
- Link state is better at avoiding loops
	- Every node knows everything, can avoid loops
	- In distance vector, each node knows a little - relying on accuracy of information from prior nodes

#### Routing between sites:
- Inter-site routing uses exterior routing protocols
	- advertise your networks prefixes to neighbouring networks
	- you may or may not offer transit to other networks
	- policy is often more important than path costs
- De facto protocol is Border Gateway Protocol (BGP)
	- Works between AS
	- Distance-Vector -like, but includes information about the AS path associated with a given route, cost of paths and other rich attributes

#### BGP AS Paths Example:
![[Pasted image 20250207103437.png]]


#### BGP Operation:
- In configuration, specify IP of neighbour and AS, e.g. Cisco:
- Creates a BGP peering session (over TCP, port 179)
	- Initially sends whole routing table, then increments updates
- Then you advertise routes you know of to your neighbours
	- Contains network prefix, prefix length, AS path, next hop...
	- Filtering can be applied to what is advertised and what is received
- Neighbour may then choose whether to use that route
	- Can use knowledge of ASNs to decide whether to accept/use the route
- You know the full path, so you can detect loops if your own AS is on a path you receive

#### BGP Downsides:
- Relies on trust
	- A malicious peer can cause issues with your routing 
- Too slow
	- Updating BGP takes a lot of effort
	- Links can go up and down for different reasons
	- Update too quickly and you get flapping
	- Default KEEPALIVE period is 60s, with a HOLDDOWN timer of 180s 
- Routers have limited BGP routing table sizes
	- Internet expansion and IPv4 exhaustion are pushing the limit of older hardware
	- For many current routers, this is ~1M Ipv4 and ~128k IPv6 routes

#### Traceroute:
- Determines the route between two hosts
- Sends packets with gradually increasing TTL
	- looks for the ICMP Time Exceeded message at each hop
	- Linux, macOS, BSD, etc. send UDP packets
	- Windows sends ICMP echo requests
- On Windows it is called "tracert"
- N.B. Traceroute does not reveal asymmetric routing, routes change over time, sometimes very quickly!

#### Routing Gotchas
- Routes across the Internet can change quickly
	- may change packet-to-packet
	- path and length may change
- Routes are quite likely to be asymmetric
	- Hence why latency  != RTT/2
- Not all routes are equal
	- Some are fast, some are slow and some have problems






# References