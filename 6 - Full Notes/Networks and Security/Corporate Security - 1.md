08-05-2025 14:15

Status:

Tags: [[Networks and Security]] [[Basic Security Concepts]] [[Corporate Security - 2]]


# Corporate Security - 1

#### UK Cyber Essentials:
- Main goal: protection against the most common cyber threats
- Not effective against advanced attacks
	- Zero-day vulnerabilities
	- Social engineering
	- Advanced persistent threats

#### Basic IT infrastructure protection requirements:
- Firewalls 
- Secure configuration
- Security update management
- User access control
- Malware protection

#### Cyber Essentials:
- First step: define the scope
	- What are the boundaries of the IT infrastructure to protect?
- The requirements apply to all software/devices within this boundary that
	- Accept incoming connections via Internet from untrusted hosts
	- Establish outbound connections via Internet
	- Control the flow of data between these devices and the Internet
- Some strategies:
	- Bring your own device (BYOD)
	- Home working 
	- Wireless devices
	- Cloud services
	- Accounts used by 3rd-parties and managed infrastructure
	- Devices used by third-parties
	- Web applications

#### Firewalls:
- Aim:
	- To make sure that only secure and necessary network services can be accessed from the internet
- Network security device
- Reduce exposure to attacks (boundary FW vs host-based FW)
- Firewall rules to block/allow traffic based on src, dst, protocol
- Requirements:
	- Block all inbound connections by default
		- Except those towards services meant to be accessed from the Internet
	- Every inbound rule that accepts connections must be motivated and documented
	- Remove or disable unnecessary firewall rules quickly, when they are no longer needed

#### Secure Configuration:
- Aim:
	- Ensure that computers and network devices are properly configured to reduce vulnerabilities and provide only the services required to fulfil their role
- Set of best practices for the configuration of computers/devices
- Default configurations are not always secure
	- Administrative account with known default password
	- Unnecessary applications and services
- Requirements:
	- Remove/disable unnecessary software
	- Disable auto-run features
	- Change default/guessable passwords
	- Ensure users are authenticated before allowing them to access data or services

#### Security Update Management:
- Aim:
	- Ensure that devices and software are not vulnerable to known security issues for which fixes are available
- Set of best practices for the maintenance and update of software
- Known vulnerabilities are likely to be exploited soon by attackers
- Vendors release patches for product they still support
	- As soon as new vulnerabilities are discovered
	- Periodically 
- Requirements:
	- All software must be licensed and supported, otherwise removed
	- Have automatic software updates enabled where possible
	- Make sure updates are applied (manually, if required) within 14 days from release
		- For high-risk vulnerabilities

#### User Access Control
- Aim:
	- Ensure that user accounts are assigned to authorised individuals only and provide access to only those assets the user needs to carry out their role
- Set of processes and techniques to manage accounts and authorisations
- Reduce the risk of information being stolen or damaged
- Compromised accounts with high privileges can result in sever damage
- Requirements:
	- Setup a process to create and approve a new user account
	- Always authenticate users before granting access to applications/devices
	- Remove/disable accounts when no longer required
	- Remove/disable special access privileges when no longer required
	- Implement MFA, where available
	- Use seperate accounts to perform administrative activities only

#### Malware Protection
- Aim:
	- To restrict execution of known malware and untrusted software, from causing damage or accessing data
- Verify if software is malicious
- Reduce the risk of damage caused by harmful code
- Potential source of malware infection: 
	- Email attachments, downloads, direct installation of unauthorised software
- Problems deriving from malware infection:
	- Malfunctioning, data loss/leakage
- Requirements for each device in scope (must use at least one of these):
	- Anti-malware software:
		- Be updated in line with vendor recommendations
		- Prevent malware from running
		- Prevent connections to malicious websites over the internet
	- Application whitelisting: only approved applications, restricted by code signing, are allowed to execute on devices
# References