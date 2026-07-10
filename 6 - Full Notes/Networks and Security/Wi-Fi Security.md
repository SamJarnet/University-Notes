14-03-2025 09:07

Status:

Tags: [[Networks and Security]] [[Wi-Fi]]


# Wi-Fi Security

#### Why do we need Wi-Fi security?
- Wireless is inherently less secure than a wired connection
	- Signal is not constrained by wires
	- Anyone within range can listen in or participate
- Risk of unauthorised access with wireless networks

#### Types of attacks:
- Eavesdropping
	![[Pasted image 20250314091014.png]]
- Man In The Middle
	![[Pasted image 20250314091040.png]]
- Deauthentication attack:
	- forces Wi-Fi devices to disconnect from a network
- Evil twin attack

#### WEP (Wired Equivalent Privacy):
- First security protocol for 802.11 wireless networks (1997)
- Intended to provide data confidentiality comparable to a wired network
- Encrypts data to eliminate eavesdropping

#### WEP: How does it work?
- Pre-Shared Key (PSK) manually set on both the client device (40-bit)
- 24-bit initialisation vector (IV) (a randomly generated value)
- RC4 (Rivest Cipher 4) stream cipher to encrypt data
- Integrity Check Value (ICV)
	![[Pasted image 20250314091501.png]]

#### WEP: why is it insecure?
- RC4 encryption is weak
- IV is too short (24-bit) and sent in plaintext along with the packet
- static pre-shared key
- Weak Integrity check (ICV)

- Proved to be insecure in the early 2000s:
	- In 2005, the FBI demonstrated that a busy WEP protected network could be cracked in 3 minutes
	- In 2007, additional techniques for generating traffic allowed a quiet network to be cracked with a 50% chance in < 1 minute

#### WPA (Wi-Fi Protected Access):
- Temporary key derived from Pre-Shared Key (PSK) using the Temporal Key Integrity Protocol (TKIP)
- RC4 kept for backwards compatibility
- key length: 128 bits
- IV extended to 48 bits

#### WPA PSK Vulnerabilities:
- Still based on RC4 encryption, which is weak
- WPA-PSK relies on a shared password making it vulnerable to:
	- Brute-force attacks (guessing passwords)
	- Dictionary attacks (common password lists)

#### WPA2 (Wi-Fi Protected Access II):
- Successor to WPA introduced in 2004
- Authentication encryption using AES (Advanced Encryption Standard) with CCMP instead of RC4

#### Key Reinstallation AttaCK (KRACK):
- A vulnerability discovered in WPA and WPA2 encryption in 2017
- Attacks force a device to reinstall an already used key, leading to the decryption of data or injection of malicious traffic
- Patch releases from manufacturers addressed KRACK vulnerabilities

#### Kr00k:
- A vulnerabilty discovered in Wi-Fi devices affecting WPA2 encryption (2019). It allows an attacker to decrypt data packets.
	- Found in devices like Raspberry Pi 3, iPhone 8, Nexus 5/6, Amazon Echo, some Asus and Huawei routers, etc.
- ~1 billion affected devices
- Fixed by a software update

#### WPA3 (Wi-Fi Protected Access 3):
- Successor to WPA2 introduced in 2018
	- AES (Advanced Encryption Standard) for encryption, just like WPA2
	- PSK replaced with SAE (Simultaneous Authentication of Equals)

#### Wi-Fi Protected Setup (WPS):
- Intended to make it easier to connect to a WPA-protected network
- User enters an 8-digit pin or presses a button on the access point for initial connection
- BUT the pin can be brute-forced quickly
- Prevailing recommendation is to disable WPS!

#### Summary 
- WEP (Wired Equivalent Privacy): first but insecure Wi-Fi encryption protocol that uses weak encryption (RC4). 
- WPA (Wi-Fi Protected Access): improved version, uses TKIP encryption and provides better security.
- WPA2 (Wi-Fi Protected Access 2): more secure, uses AES encryption, but is vulnerable to some attacks like KRACK if not properly updated. 
- WPA3 (Wi-Fi Protected Access 3): latest Wi-Fi security standard, with enhanced security features like Simultaneous Authentication of Equals (SAE).
# References
