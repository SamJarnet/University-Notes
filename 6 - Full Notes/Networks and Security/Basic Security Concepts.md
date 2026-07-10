22-04-2025 13:48

Status:

Tags: [[Networks and Security]]


# Basic Security Concepts

#### Cyber Security C.I.A Triad

- The three security objectives for information and information systems.
- Confidentiality:
	- Preserving unauthorised restrictions on information access and disclosure, including means for protecting personal privacy and proprietary information.
		- A loss of confidentiality is the unauthorised disclosure of information
- Integrity: 
	- Guarding against improper information modification or destruction, including ensuring information non-repudiation ( a party cannot deny having sent a message, signed a document, or performed an action) and authenticity.
	- Making sure that the application loss of an information system is not altered inappropriately.
		- A loss of integrity is the unauthorised modification or destruction of information, or the unauthorised modification of information systems
- Availability:
	- Ensuring timely and reliable access to and use of information.
		- A loss of availability is the disruption of access to or use of information or an information system


#### Integrity-related Concepts
- Authenticity: property of being genuine and being able to be verified and trusted
	- Confidence in the validity of a transmission, a message, or message originator
	- This means that verifying that
		- Users are who they say they are
		- Each input arriving at the system comes from a trusted source
- Accountability: security goal that generates the requirement for actions to be traced uniquely to that entity
	- This supports non-repudiation, deterrence, fault isolation, intrusion detection and prevention, and after-action recovery and legal action
	- Because truly secure systems are not yet an achievable goal, we must be able to trace a security breach to a responsible party
	- Systems must keep records of their activities to permit later forensic analysis to trace security breaches or to aid in transaction disputes

#### A Model of Computer Security:
- Asset, or system resource.
	- Hardware:
		- Including Computer Systems and other data processing, data Storage, and data communications devices
	- Software:
		- Including the [[Operating Systems]], system, system utilities, and applications.
	- Data: 
		- Including files and databases, as well as security-related data (e.g. passwords).
	- Communication facilities and networks:
		- Local and wide area network communication links, bridges and so on.
	![[Pasted image 20250422145106.png]]

- Types of asset vulnerabilities:
	- The system can be corrupted, so it does the wrong thing or gives the wrong answers
		- For example, stored data values may differ from what they should be because they have been improperly modified
	- The system can become leaky
		- For example, someone who should not have access to some or all of the information available through the network obtains such access
	- The system can become unstable or very slow
		- For example, using the system or network becomes impossible or impractical

- Each vulnerability might correspond to a threat capable of exploiting it
	- A threat represents a potential security harm to an asset

- An attack occurs when a threat materialises:
	- If successful, leads to an undesirable violation of security
	- The agent executing the attack is referred to as an attacker, threat agent or adversary
- Attack classification based on type of impact to assets
	- Active attack: An attempt to alter assets or affect their operation
	- Passive attack: An attempt to learn or make use of information from the system that does not affect assets
- Attack classification based on attack origin:
	- Inside attack: Initiated by an entity inside the security perimeter (an "insider"). The insider is authorised to access system resources but uses them in a malicious way
	- Outside attack: Initiated from outside the perimeter, by an unauthorised or illegitimate user of the system (an "outsider)

- Risk is a measure of the extent to which an asset is threatened by a potential circumstance or event, and typically a function of
	- The adverse impacts that would arise if the circumstance or event occurs
	- The likelihood of occurance
- A countermeasure is any means taken to deal with a security threat/attack
	- Detection
	- Prevention
	- Mitigation 
	- Recovery

#### Threats and Assets
![[Pasted image 20250422151132.png]]
# References