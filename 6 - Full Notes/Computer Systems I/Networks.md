03-11-2024 21:03

Status:

Tags: [[Computer Systems I]]


# Networks 1

#### What is a Network?
- Multiple computers that are connected together and can share information and/or recourses
- The Internet is a network of networks
- N.B. - the Internet != the World Wide Web

#### Common Terms:
- WAN: Wide Area Network
	- A network that extends over a large geographical area
- LAN: Local Area Network 
	- A network that covers a small geographical area
- MAN: Metropolitan Area Network
- PAN: Personal Area Network
	- Short-range network around a person

#### Layered Network Models:
Two main models:
- OSI model
- TCP/IP model
TCP/IP Model:
	- Application Layer
	- Transport Layer
	- Internet Layer
	- Network Access Layer

Why a layered model?
- Abstraction
- Irrespective of the underlying hardware and topology:
	- Applications can talk to each other
	- Host can talk to each other

#### The End-to-End Concept:
- The network:
	- Is responsible for providing best-effort connections
	- should be essentially transparent
- End hosts are responsible for reliability and security

#### Layer Encapsulation
- Each layer in the TCP/IP stack adds it's own header to the data
- This becomes the payload for the next layer

#### Network Access Layer:
- Deals with the local link that a host is connected to
- Each host has a link-unique address (48-bit MAC address)

#### Internet Layer:
- Three basic functions:
	- Handles next-hop routing
	- Handles unique addressing
	- Passes  a received packet's payload to the correct transport layer
-  Facilitates connection of different types of network
- The internet layer only provides a "best-effort" packet delivery
- Five main protocols: IPv6, IPv4, ICMPv6, ICMP and IPSEC 
#### IPv4:
Internet Protocols version 4:
- Each node has unique 32-bit IP address
- Written in octet-grouped dotted-decimal notation
	- e.g. 152.78.65.112
- Variable length header, minimum of 20-bytes
IPv4 Exhaustion:
- 32-bit address space = about 4.3 billion addresses
- Exhaustion anticipated since the 1980s
- IANA allocated their last blocks to RIRs on 3/02/2011
- Two "solutions":
	- Network Address Translation (NAT) (1993)
	- Address reclamation/recycling
	- IPv6 (1998)
	
#### NAT & NAPT:
- A way to share one IPv4 address between multiple computers
	- e.g. a home router shares one public IPv4 address with multiple devices with private IPv4 addresses 
- RFC1918 "private" address space:
	- 192.168.0.0/16, 10.0.0.0/8 and 172.16.0.0/16
- Not a real solution:
	- NAPT breaks the end-to-end principle and some protocols
	- Even with NAT, we still have IPv4 exhaustion
	- Gives a false sense of security - NAT is not a replacement for a properly configured firewall

#### Address Recycling:
- There is a booming market in used IP address space
	- ~$50 per address
- Some registrars can only give you recycled address space

#### IPv6:
- Internet Protocol version 6
- Each node has a unique 128-bit IP address
- Written in colon-delimited hexadecimal
	- e.g. 2001:630:d0:f111:e07a:b1fa:68a1:80eb

#### Subnets:
- You will come across addresses written like 2001:630:d0::/64
- For IPv4 you might see something like "192.168.0.0/24" or with another number like "255.255.255.0" following them
- These indicate how many bits of the address are shared by computers in the same subnet
- A subnet(work) is a logical subdivision of a network
- Traffic between two subnets has to go via a router

#### Routing:
- Occurs where there is a change in IP address spaces
- Routing occurs at the internet layer
- Each router has an IP address in each address space it routes between
- Routers can also have other functions:
	- Firewalling, DNS, DHCP, etc.
- There can be multiple possible paths between two hosts
- This is for redundancy, improved performance of commercial reasons
- Internet: managed by BGP
- "Local": usually OSPFv3

#### Transport Layer:
- Provides host-to-host communication
- Two main protocols:
	- TCP = Transmission Control Protocol
	- UDP = User Datagram Protocol
- Some other specialised protocols:
	- Point to Point Tunnelling Protocol
	- CubeSat Space Protocol

#### TCP and UDP:

![[Pasted image 20241104112438.png]]

#### TCP Flow/Congestion Control:
- Flow Control (a):
	- Prevents a fast sender overwhelming a slow receiver
- Congestion Control (b):
	- Reduces send rate to cope with network congestion

#### TCP flow control:
- TCP uses a sliding window protocol to control the sending rate
- Sender should only send if the receiver indicates it has buffer space to accept data
- The sliding window is effectively the buffer space the receiver says it has available

#### Congestion Control:
- Sender starts by sending small packets
- Sender increases the size of each subsequent packet until there is packet loss
	- Exponentially until it hits a threshold, then additively
- Sender restarts the cycle with a lower threshold
- Causes TCP's typical sawtooth throughput

#### Application Layer:
- Software that uses the network
- Generally, programmers will use pre-made libraries BUT need to choose appropriate modes.

[[Networks 2]]

# References