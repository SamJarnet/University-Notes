07-02-2025 09:14

Status:

Tags: [[Networks and Security]] [[Subnets]]


# NAT

#### RFC 1918:
- We don't have enough IPv4 addresses to give every device a globally unique address
- RFC 1918 private addresses can be used for private networks. These addresses are not globally routable!
	- 10.0.0.0/8, 16 million addresses
	- 172.16.0.0/12, 1 million addresses
	- 192.168.0.0/16, 65k addresses
- Relatedly, RFC 7335 defines 192.0.0.0/29 for IPv6 transition mechanisms, e.g. for CLAT

#### NAT:
- You have an IPv4 network that uses private addresses but need Internet access, what do you do?
	- Share a global IPv4 address between multiple hosts
- Architectural price and performance overhead
- Really Network Address and Port Translation (NAPT), but NAT is commonly used to refer to it 
	![[Pasted image 20250207093515.png]]
#### CGNAT (RFC6598):
- ISPs have been running out of IP addresses
- Many are now doing Carrier-Grade NAT:
	- Share a small number of global addresses between customers.
	- Customers get a private address from RFC6598 (100.64.0.0/10)
	- Customers then NATs that address to RFC1918
	![[Pasted image 20250207093841.png]]


[[Routing]]
# References