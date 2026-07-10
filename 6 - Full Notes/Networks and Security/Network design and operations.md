22-04-2025 15:42

Status:

Tags: [[Networks and Security]]


# Network design and operations

#### Internet:
- Global public network connecting devices worldwide using standardised protocols (TCP/IP)
- Enables communication, information sharing and online services
- Accessible to anyone with an internet connection
- Security risks: lack of content control, privacy concern, vulnerable to hacking and malware

#### Intranet:
- A private network that is restricted to an organisation's employees. It is used for sharing information, resources and tools within the organisation
	- Accessible only by authorised personnel
	- Can host internal websites, forums, and communication tools
	- Secure isolated from public internet threats (firewalls and VPN)

#### Extranet: 
- A private network that extends certain services or access to external partners, clients or suppliers
	- Provides controlled access to specific resources and information 
	- Accessible to external parties with restricted permissions
	- Often used for collaboration between different organisations

#### Intranet/Extranet: 
![[Pasted image 20250422154716.png]]

#### What keeps an intranet/extranet secure?
- Access Controls: Ensures only authorised internal users can access certain resources (role-based)
- Encryption: Protects data being transmitted across the network (e.g. SSL/TSL for web communication)
- Firewalls and VPNs: To protect against unauthorised access from the public internet

#### Firewalls:
- If the packet matches an allowed rule, it is forwarded. If not, it is blocked
- For instance:
	- Allows traffic from trusted IP addresses
	- Block all incoming traffic on port 80 (HTTP)

#### Virtual Private Network (VPN):
- A VPN creates a secure connection between a user and the internet. protecting data from external threats
- How does it work?
	- The user connects to the service
	- The VPN client encrypts data before it leaves the device
	- Data is sent through a secure tunnel to the VPN server
	- The VPN server decrypts the data and forwards it to the destination
	- Response from the destination is encrypted and set back to the user via the same secure tunnel

#### Why use a VPN?
- Security: a VPN encrypts your internet traffic and protects sensitive data
- Privacy: Masks your IP address to ensure anonymity 
- Bypass geo-restrictions and censorship: Access region-restricted content by connecting to VPN servers in different countries
- Secure remote access: Allows employees to securely access company recourses from remote locations 

#### Limitations: 
- Performance issues: VPNs can slow down internet speeds due to encryption overhead
- Complexity and Management: cost of developing and maintaining, especially for many endpoints
- Security risks: a VPN only encrypts data between your device and the VPN server and does not ensure end-to-end encryption. 

#### Types of VPN protocols:
- PPTP (Point-to-Point Tunnelling Protocol): Older, faster but less secure
- L2TP/IPSec(Layer 2 Tunnelling Protocol with IPsec): More secure, more commonly used
- IKEv2/IPSec(Internet Key Exchange version 2): Very fast, secure, and ideal for mobile device






# References