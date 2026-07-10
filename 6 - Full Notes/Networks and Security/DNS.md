14-02-2025 09:01

Status:

Tags: [[Networks and Security]] 


# DNS

#### DNS Reminder:
- DNS maps host/domain names to IP addresses
- e.g. for glacsweb.org:
	![[Pasted image 20250214090243.png]]
- It can also map IP addresses to domain names:
	![[Pasted image 20250214090319.png]]

#### Why do we need DNS?
- A text file (HOSTS.TXT) was originally used for name resolution on ARPAnet.
	- Used to populate /etc/hosts on [[UNIX]]
- Started being a problem in 1980s:
	- SRI-NIC traffic and load
	- Name collisions
	- Size of file
	- Resiliency

#### DNS Overview:
- DNS is a distributed, hierarchical system
- Operates on port 53, mostly UDP
- Domain names are delegated from ICANN through the Top Level Domain (TLD) registrars
- e.g. for uglogin.soton.ac.uk
	- Nominet control the .uk TLD
	- and delegate "ac.uk" to JISC
	- who delegate "soton.ac.uk" to the University
	- who host an authoritative name server and can create a record for "uglogin.soton.ac.uk"

#### DNS Record Types:
![[Pasted image 20250214090813.png]]

#### Looking up Data in DNS:
- The most common DNS lookup is host name to IP
	- Hosts query DNS for A record (IPv4) and/or AAAA record (IPv6)
- This implicitly requires that clients know about (local) DNS server they can send queries to:
	- May be the ADSL router in a home network
	- Or a DNS server run by iSolutions on the campus
	- There are also "public" DNS servers 
0
#### DNS Terminology: 
- A resolver is a program that extracts information from name servers. They "resolve" the query and return the answer
- Servers have different modes:
	- Iterative where it responds with a referral to another server
	- Recursive where it responds from local cache or resolves the query before replying to the client
		- Can be thought of as having a DNS server side and a resolver side
- A forwarder sends queries to a different DNS server, even if the RD bit is set. Think DNS proxy

#### Clients DNS Configuration:
- Network clients are configured to use one or more local DNS servers
	- Usually sent by SLAAC, DHCPv6 or DHCP
	- Can be specified manually

#### Looking up DNS entries:
- An application writer can use APIs to do DNS lookups
	- e.g. getaddrinfo() in POSIX, returns an addrinfo struct from name
	![[Pasted image 20250214092104.png]]

#### DNS Utilities:
- You can use a command line tool to look at DNS entries, e.g. dig:
	![[Pasted image 20250214092139.png]]

#### Phone numbers in DNS?
- DNS isn't just for looking up IP addresses
- TXT records are used for domain verification, SPF records, site verification, etc.
- eduroam depends on NAPTR records
- Also includes ENUM for IP telephony

#### Hierarchy:
- Each node stores names that end with the same suffix
	![[Pasted image 20250214092853.png]]


#### DNS Zone:
- A DNS Zone is a continuous chunk of name space:
	- Complete tree, subtree or single node
- Each zone has an associated set of name servers
	- Stores list of names and tree links
	![[Pasted image 20250214093239.png]]

#### Domain Name Space:
- ![[Pasted image 20250214093415.png]]

#### Zone Delegation:
- Zones require the owner to delegate a subzone
	- You need to "convince" them to do it somehow
- Records within a zone should be stored redundantly:
	- Manually update primary name server
	- Secondary name servers updated by zone transfer

#### Root Nameservers:
- Responsible for the "root" zone
- Currently 13: {a-m}.root-servers.net
- Operated by 12 independent organisations
- Queried when local name servers can't resolve a name

#### A resilient DNS?
- The DNS is a critical Internet infrastructure
	- Along with the routing infrastructure!
- The DNS is therefore a target which some people may try to attack
- We therefore need to make the DNS resilient to such attacks 
	- Especially the DNS root servers

#### Root Nameserver Resilience:
- Root servers are required as the "anchor" for recursive DNS
- In practice there are 1730+ distributed DNS servers

#### Anycast:
- Allows a client to reach the nearest instance of a service
- You can advertise the same IP, or small IP block, at multiple points of the Internet
- Routers then learn of the nearest instance, topologically via the [[Routing]] system (typically BGP)
- This means you will access a different instance, depending on where you are
	- Whether making genuine DNS queries, or trying to attack DNS
	- If one instance is down, you should pick up the next nearest

#### Typically Recursive Resolution:
![[Pasted image 20250214094140.png]]


#### What your computer does:
- In practice, "we" don't talk to the root servers much
	![[Pasted image 20250214094228.png]]
- Using caches reduces queries to external DNS servers
- DNS records have a TTL, typically 1 to 72 hours

#### Public DNS servers:
- Usually DNS name servers should be configured to only answer external queries for their own internal domains
	- e.g. ECS DNS servers should only answer external queries for hosts under ecs.soton.ac.uk
- There are open public servers though
	- Google DNS
	- Cloudfare
	- Quad9
- Can be useful if your organisation does DNS filtering
#### DNS and privacy?
- All traffic we generate can be viewed by a third party "tapping" the communication path

#### mDNS (RFC6762):
- Not every network needs full DNS infrastructure 
- Small (e.g. home...) networks benefit from "zero configuration" approaches
- Enter multicast DNS:
	- Essentially local DNS without a DNS server
	- Works by sending multicast packets to ff02::fb or 224.0.0.251 on UDP port 5353
	- Implemented by Bonjour (Apple), Avahi (open source) and in Windows




# References