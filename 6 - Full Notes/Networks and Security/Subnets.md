07-02-2025 09:00

Status:

Tags: [[Networks and Security]]


# Subnets

#### The Internet (TCP/IP)/Network Layer (OSI):
- Second layer in the TCP/IP
- Known as the Network Layer (Layer 3) in the OSI modl
- Each device has a globally unique IP address
- At this level, networks are divided into subnets

#### Subnets:
- We want to limit the propagation of Ethernet broadcast traffic and segment hosts
- We can subnet a larger IP allocation to logically divide the network:
	- e.g. for a campus, typically subnet on a per-building or per-department basis
	- And for IPv4 we should size them for the umber of devices
#### Available Addresses in an IPv4 Subnet:
- Not all addresses in a subnet are usable!
	- First addresses is reserved
	- Last address is the broadcast address
	- One address is required for the router (typically the first or last usable address)
- e.g. 152.78.70.0/24:
	- 256 total addresses
	- 152.78.70.0, 152.78.70.255 are reserved 254 usable
	- 152.78.70.1 or .254 for the router, 253 left

#### IPv4 Subnet example:
- I have an allocation of 152.78.70.0/23 and I want to make three subnets.
	- One subnet has 200 devices and the other two have 100 devices each
- For 200 devices, I need a /24 (254 addresses)
- For 100 devices, I need a /25 (126 addresses)
- So I can do: 
	- 152.78.70.0/24
	- 152.78.71.0/25
	- 152.78.71.128/25

[[NAT]]




# References