04-11-2024 11:34

Status:

Tags: [[Computer Systems I]] 


# Networks 2

[[Networks]]

#### ICMP/ICMPv6:
- Used for diagnostic and control purposes or generated in response to errors in IP operation
- Contained within a standard IP packet
	- ICMP works with IPv4
	- ICMPv6 works with IPv6
- Used by Ping and Traceroute

#### Naming and Addressing:
- Each layer uses different addressing:

![[Pasted image 20241104113739.png]]

- Using IP addresses in applications can be problematic
	- What if you change host or ISP? What if you change protocol
- How do you map hostname to IP address and IP address to MAC address?

#### ARP/NDP
- Address Resolution Protocol (IPv4)
- Neighbour Discovery Protocol (IPv6)
- Operates at the Link Layer
- Translates IP addresses to MAC addresses
- You can find a MAC address for a given IP with the arp command

#### DNS:
- Domain Name Service provides a way to map symbolic domain names to an IPv4 or IPv6 address
- Highly-reliable and resilient distributed service
- Operates at the Application Layer
![[Pasted image 20241104114140.png]]

#### How do we make a network bigger?
- Point-to-Point links are great, but we want to talk to lots of different computers
- One way to add more ports is a hub:
	- Essentially a multi-port repeater
	- All computers connected to the hub get all of the packets
	- Largely obsolete these days

#### Switches:
- Used to connect multiple devices on one network segment
- Switches operate at the Network Access-Layer
- A switch only forwards traffic between the ports it needs to

#### Getting IPv6:
- Many home ISPs support IPv6
- You can use a tunnelbroker to get working IPv6 on an IPv4 connection:
	- Hurricane Electric
- Tunnels IPv6 over IPv4
- Higher latency than a native IPv6 connection

#### Monitoring:
- Everything you do on the Internet generates a log somewhere:
	- Network owners need/want to know what is happening on their network
	- Governments want to know what people are doing 
- In the UK, ISPs can be required to store certain connection information. New legislation is being considered to expand the extent of this logging

#### Staying Anonymous:
- "anonymous" VPNs:
	- Still creates logs somewhere
	- VPN exit point can be monitored 
- ToR - "The Onion Router"
	- Routes traffic through a (random) series of hops
	- Traffic is encrypted to the exit node
	- Reduces performance
	- Not fool proof: Vulnerable to traffic analysis & exit node monitoring
	- Contains other exploitable vulnerabilities
# References