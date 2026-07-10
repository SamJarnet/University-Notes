21-03-2025 09:19

Status:

Tags: [[Networks and Security]]


# Public Key Infrastructure

#### Digital Certificates:
- Binds a user/company identity to its public key
- Standard: X.509
	![[Pasted image 20250321092116.png]]
- Used in:
	- Secure email
	- VPNs
	- Wi-Fi
	- Web Servers
	- Network Authentication
	- Code signing

#### Public Key Infrastructure:
- The set of hardware, software, people, processes, policies and procedures
- Needed to create, manage, store, distribute and revoke digital certificates based on asymmetric cryptography
- To enable secure, convenient, and efficient acquisition of public keys

#### Certification Authority:
- Responsible for issuing, revoking and distributing public key certificates
- Often trusted-third party organisation
	- VeriSign, DigiCert and Comodo
- Certificates are signed with a CA's private key
	- Thus, everybody can check the authenticity of the certificates
	- By using the CA's public key (as for checking the digital signature)
		- Browsers have installed the public keys of all the major CAs
- Important to protect the CA's private key

#### Registration Authority (RA):
- Performs functions for CA but does not issue certificates directly
	- Identification and authentication of certificate applicants
	- Approval or rejection of certificate applications
	- Initiating certificate revocations and suspensions under certain circumstances
	- Processing subscriber requests to revoke to revoke or suspend their certificates
	- Approving or rejecting requests by new subscribers to renew or re-key their certificates
#### PKI Repositories:
- Means of storing and distributing certificates and certificate revocation lists (CRLs) and managing updates to certificates
- Allow relying parties to retrieve certificates and CRLs

#### Certificate Issuance & Usage:
- Issuance
	- RA verifies subject information
	- Generate Public - Private Key Pair
	- CA issues the certificate
- Usage: relying party wants to verify a signature
	- Fetch the certificate
	- Fetch certificate revocation list (CRL)
	- Check the certificate against CRL
		- Is the certificate valid or is it revoked?
	- Check the signature using the certificate

#### Life Cycle of Certificates:
![[Pasted image 20250321093108.png]]

#### Certificate revocation list:
- It is a list of certificates which are no longer valid
- Published regularly by the CA in the PKI repository
- But also sent to any relying party who has subscribed to it 
- Problems:
	- Not issued frequently enough to be effective against an attacker
	- Expensive to distribute
	- Vulnerable to simple DoS attacks

#### X.509:
- The most widely accepted format for public-key certificates
	- Used in most network security applications
	- Such IP security (IPSEC), secure socket layer (SSL), and transport layer security (TLS)
- Issuer: CA
- Subject: Public Key Owner 
- Signature: Hash of the entire block signed by the CA's private key

#### X.509 Certification Revocation List:
- Each revoked certificate entry contains a serial number of a certificate and the revocation date
- Due to overheads in retrieving and storing these lists:
	- Very few applications use this 
- A more practical alternative is Online Certificate Status Protocol (OCSP):
	- Query the CA as to whether a specific certificate is valid


# References