09-05-2025 08:57

Status:

Tags: [[Corporate Security - 1]] [[Networks and Security]] [[Basic Security Concepts]]


# Corporate Security - 2

#### Data Protection:
- Understand the risk:
	- What data?
	- Who would want it?
	- What would be the impact?
- Use encryption:
	- Data at rest and in transit
	- Key management
- Fragmentation:
	- Split data into multiple pieces, stored in diverse locations
	- Harder for an attacker to collect all the fragments
- Data Backup:
	- Frequently make copies of data
	- Keep backup data on different, seperate devices
- Privacy Protection:
	- Sanitize information to remove PII

#### Segregation of Duties:
- Basic idea:
	- Have more than one person required to complete a critical task
- Application in Cyber Security:
	- If N accounts are required to execute a security-critical task, then N accounts should be compromised to undermine that task
- Example in banking:
	- Every sensitive order must be signed off by at least 2 different people, from 2 different departments

#### Network Fragmentation & Monitoring:
- Split infrastructure based on:
	- Business processes
	- Necessary exposure
	- Risk levels
- Examples:
	- Offices need access to the internet
	- Front-end needs to be accessed from Internet
	- Back-end only accessed by privileged users
- Use firewalls at all boundaries:
	- Beware of reconfigurations

- Network monitoring - Intrusion Detection/Prevention Systems (ID/PS):
	- Observe/record all traffic on a given network
	- Detect/block malicious traffic
	- Signature-based vs anomaly-based
	- Alert on suspicious traffic
- Example: an unknown computer starts scanning the whole address space
	- An intruder?
	- An admin with a new tool?
	- A third-party contractor doing maintenance?
- Use machine learning techniques:
	- Accuracy
	- Explainability
	- Adversarial learning

#### Honeypots:
- A decoy to lure attackers:
	- Hardware, Software and data to simulate a real system, actually isolated
	- Attack detection
	- Deflect attackers
	- Gather valuable info on attack strategies
- Research/production honeypots
	- Beware of effective isolation in production honeypots!
- High-interaction/low interaction honeypots

#### Pentesting:
- Authorised simulated attack, aimed at assessing the security of a system
	- One of the most effective way to find vulnerabilities
	- Can identify how an attacker could compromise the system
	- Frameworks exist to automate and ease common pentesting operations
- Penetration Testing Execution Standard (PTES):
	- Adopted by several authoritative members of security community
	- Goals:
		- Fostering awareness about the importance of pentesting
		- Establishing fundamental principles for carrying out a pentest
- Phases of Pentesting:
	- Pre-engagement interaction (goals definition)
	- Intelligence Gathering (what security mechanisms are being used?)
	- Threat Modelling (how can I attack the target in practice?)
	- Exploitation (the actual attack)
	- Post Exploitation (what can I do once the target has been compromised)

#### Standards:
- ISO 27000 series, NIST 800 series:
	- Big, generic and complicated
	- Appropriate for big businesses only
	- In comparison: cyber essentials ~ 10 pages
- Specific standards for specific industries 
	- Payment Card Industry Data Security Standard (PCI DSS) 
	- Health Insurance Portability and Accountability Act (HIPAA)
- Compliance-driven security is dangerous! 
- Yet standards are an efficient stick to drive adoption
# References