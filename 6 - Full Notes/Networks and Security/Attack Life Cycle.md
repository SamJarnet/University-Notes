06-05-2025 21:40

Status:

Tags: [[Networks and Security]] [[Cyber Attacks 2]]


# Attack Life Cycle

#### Cyber-Attack Life Cycle Models:
- Empirical models representing the sequence of steps that cyber attacks go through
- They provide a framework to better understand cyber attacks to:
	- Figure out why past attacks succeeded
	- Develop a structured knowledge base on past attacks
	- Identify convenient and effective ways to protect assets
	- Forecast potential next steps of a possibly ongoing attack

#### Lockheed Martin's Kill Chain Model:
- Seven layers of the model:
	- Reconnaissance
	- Weaponization
	- Delivery
	- Exploitation
	- Installation
	- Command & Control (C2)
	- Action on Objectives

#### Reconnaissance:
- Target research and selection
- What information did the attackers gather? How?
- Examples:
	- Crawling of websites to gather email addresses
	- Scans and probes to identify the security means used by the target

#### Weaponization:
- Development of required cyber weapons, coupling exploit with backdoor into deliverable payload
	- E.g. Malicious payload, paired with an exploit
- What cyber weapons have been used? How did the attackers obtain them?
- Examples:
	- PDF or Microsoft Office documents with embedded malicious scripts
	- Remote Access Trojan (RAT)
	- Stolen credentials
	- Setup the C2 infrastructure
	- Phishing email

#### Delivery: 
- Delivery of the payload to the target
- How did the attackers deliver the cyber weapon(s) to the target?
- What was delivered, from where to where and how?
- Examples:
	- Download from website
	- Email attachment
	- USB stick

#### Exploitation:
- Execution of the payload, e.g. through exploiting a vulnerability
- How were cyber weapons activated?
- Examples:
	- Exploit of known vulnerabilities of the target
	- Exploit of OS auto-start feature
	- User deception

#### Installation:
- Ensure payload persistence within the target
- How did the attackers gain persistence inside the target?
	- E.g. how did the attackers make sure that the cyber weapon would execute again after a reboot?
- Examples:
	- Multiple copies installed in different machines
	- Register the malicious payload as OS service with auto-start mode

#### Command & Control (C2):
- Establish a communication channel with an external command and control (C2) server to remotely manipulate the victim
- How did the attackers establish a communication channel to control the cyber weapons installed inside the target?
- Examples:
	- Ciphered connection over HTTPS
	- Information exchange through public, beyond suspicion channels (e.g. on Twitter through tweets having specific hashtags)

#### Actions on Objectives:
- Execution of desired actions within the target, based on commands from C2
- What did the attackers do to achieve their goals?
- Examples:
	- Data exfiltration
	- Disruption

#### Multi-Step Cyber-Attacks:
- Lateral movement:
	- The attackers use existing vulnerable systems that are connected to the final target
	- They attack the vulnerable connected systems and move laterally to the intended target after they have access to the connected systems
	- Data can be exfiltrated after the process is completed 

# References