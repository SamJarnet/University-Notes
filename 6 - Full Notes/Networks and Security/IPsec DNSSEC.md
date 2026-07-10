21-03-2025 10:03

Status:

Tags: [[Networks and Security]] [[DNS]]


# IPsec DNSSEC

#### Internet Protocol Security (IPsec):
- Designed to secure communications over IP networks by providing encryption, authentication and data integrity

#### Why do we need IPsec?
- Lack of encryption:
	- Data transmitted over a network can be intercepted and read by unauthorised parties (eavesdropping)
- No data integrity:
	- Data could be altered or tampered with during transmission
- Lack of authentication: 
	- Attackers could impersonate legitimate users or devices, allowing them to gain unauthorised access to sensitive data or systems

#### How does IPsec work?
- Authentication Header (AH): attaches a cryptographic hash (HMAC, Hash-Based Message Authentication Code), built from a shared secret key and a hash function to the packet
	- Provides data integrity and authentication
	- Does not encrypt data, so it doesn't provide confidentiality

- Encapsulating Security Payload (ESP): encapsulates the original data within a secure header and encrypts it (e.g. AES)
	- Integrity and authentication are verified through hashes and cryptographic signatures 
	- Provides encryption for confidentiality
	- Can be used with or without encryption, depending on configuration

- Internet Key Exchange (IKE): securely establishes authentication and key exchange between two devices, creating Security Associations (SAs ) to enable encrypted communication
	- Ensures the confidentiality, integrity and authenticity of the connection

- Transport mode:
	- Only the payload (data) is encrypted/authenticated
	- The original IP header remains intact and visible
- Tunnel mode:
	- Entire original IP packet (header + payload) is encapsulated and encrypted/authenticated 
	![[Pasted image 20250321102007.png]]

#### What are the downsides of IPsec?
- Performance overhead:
	- Can introduce latency due to encryption and decryption processes
- Requires complex setup and configuration
- Incompatibility issues may arise with some network devices if not properly configured

#### Reminder: DNS maps host/domain names to IP addresses:
![[Pasted image 20250321102413.png]]

#### Why do we need DNSSEC?
- DNS provides no authenticity or integrity: an attacker can divert traffic for domain to its own servers by:
	- Impersonating a resolver and returning false DNS records (DNS spoofing)
	- Forging responses from an authoritative server and poison a resolver DNS cache (DNS cache poisoning)
	![[Pasted image 20250422153432.png]]

#### Domain Name System Security Extensions (DNSSEC):
- A set of security protocols designed to add integrity and authenticity to the DNS

#### How does DNSSEC work?
- DNSSEC uses public-key cryptography to digitally sign DNS records:
	- RRSIG (Resource Record Signature): digital signature for a DNS record set
	- DNSKEY (DNS Key): public key used for verification
	![[Pasted image 20250422153658.png]]

#### Why does DNSSEC work?
- Authenticity: 
	- DNSSEC uses digital signatures to ensure that DNS responses come from the right source and have not been forged or altered
- Data Integrity: 
	- DNSSEC prevents tampering with DNS records during transmission by validating the digital signatures
- Nonexistence Proof: 
	- DNSSEC provides cryptographic proof for non-existent domains or records, preventing attackers from creating fake responses

#### What are the downsides of DNSSEC?
- No confidentiality:
	- DNS queries and responses are sent in plaintext (no encryption) and eavesdroppers can learn which domains a client resolves /visits
		- Solved by NDS over TLS (DoT) and DNS over HTTPS (DoH)
- Performance overhead


# References