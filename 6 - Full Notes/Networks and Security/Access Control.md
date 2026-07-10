28-02-2025 10:02

Status:

Tags: [[Networks and Security]]


# Access Control

#### What is Access Control?
- The process of granting or denying specific requests to:
	- 1. Obtain and use information and related information processing services
	- 2. Enter specific physical facilities
		- NISTIR 7298, Glossary of Key Information Security Terms
- A process by which use of system resources is regulated according to a security policy and is permitted only by authorised entities (users, programs, processes or other systems) according to that policy
	- RFC 4949, Internet Security Glossary

#### Access Control Principles:
- To prevent unauthorised users from gaining access to resources
- To prevent legitimate users to access resources in an unauthorised manner
- To enable legitimate users to access resources in an authorised manner
- Access control implements a security policy that specificies who or what (e.g. in a case of a process) may have access to each system resources, and what type of access that is permitted in each instance

#### Access Control Context:
- Authentication
	- Verification that the credentials of a users or other system entity are valid
- Authorisation
	- The granting of a right or permission to a system entity to access a system resource
- Audit
	- An independent review and examination of system record and activities 

#### Policies and Models:
- A security policy defines what is allowed 
	- It defines those executions of a system that are acceptable, or complementarily, those that are not acceptable
	- It is analogous to a set of laws
	- Defines in terms of high-level rules or requirements
	- Policies are measurable and can be enforced locally or in a network
- A security model provides a formal representation of a class of systems, highlighting their security features at some chosen level of abstraction
	- More simply, they are abstract descriptions of system behaviours, and can serve to guide the design of specific policies

#### Subjects, Objects and Access Rights:
- A subject
	- An entity capable of accessing objects
	- A process that represents a user or application actually gains access to an object
	- Three classes of subject: owner, group and world
- An object:
	- A resource to which access is controlled 
	- An entity used to contain and/or receive information
- An access right
	- The way in which a subject may access an object
	- Read, write, execute, delete, create and search

#### Access Control Models:
- Access control models are used to:
	- Define a specific set of authorisation rights
	- Define a set of policies for a software system to enforce a set of rights to fulfil the security concerns 
	- Protect for all multi-user systems, against violation of:
		- Confidentiality (e.g. unauthorised disclosure)
		- Integrity (e.g. improper modifications)
		- Availability (e.g. service disruption)
- The main models of access control:
	- Discretionary Access Control (DAC)
		- Based on the identity of the requestor
	- Mandatory Access Control (MAC)
		- Based on comparing security labels
	- Role-Based Access Control (RBAC)
		- Based on the roles
	- Attribute-based Access Control (ABAC)
		- Based on attributes of the subject/object and environment
- Those models are not mutually exclusive, and an access control mechanism can employ two or even more to cover different classes of system resources

#### Discretionary Access Control (DAC):
- Identity-based controls
- Every object has:
	- 1. An owner
	- 2. A discretionary access control list (DACL)
- DACLs form an access matrix
	![[Pasted image 20250228102337.png]]

- Principle: 
	- Users own resources and control their access
	- Owner may change object's permissions at its discretion
	- Owners may also be able to transfer ownership to other users
- The owner has control DACL
- The owner has the discretion to determine which subjects can have which permissions to access an object

#### Issues around DAC
- Flexible, but open to mistakes, negligence or abuse
	- Requires that all users understand mechanisms and understand and respect the security policy
- Managing the policies for a large system is a complex task
- Difficult to understand the correct access are provided to the right users
- The objects and subjects change frequently, thus also their permissions need to change
- Access matrix represents the explicit access relation between each individual subject and object, it grows very large very quickly

#### Mandatory Access Control (MAC)
- Classification of subjects and objects by security levels
	- Every subject has a profile, which includes their clearance and their need-to-know
	- Every object has a security label composed of two parts: classification (e.g. sensitivity of the data) and a category (enforcement of need-to-know)
	- AC decisions are formalised (and controlled) by comparing security labels indicating sensitivity/criticality of objects with formal authorisation (i.e. security clearences of subjects) 
- MAC policies often identified with multi-level security policies
- MAC requires careful planning and continuous monitoring to keep all resource object's and user's classifications up to date
- MAC helps prevent data leakage, making it suitable for environments where information confidentiality and integrity are critical
- Example from the military:
	- Users and objects assigned a clearance level like secret, top secret, etc.
	- Users can only read/write objects of equal or lower/higher levels
- Concrete examples: Bell-LaPadula and Biba
- More rigid than DAC, but also more secure
	- Stronger security but less operational flexibility
- Mandatory because subjects may not transfer their access rights
- Shifts power from users to system owner


#### Role-Based Access Control (RBAC):
- Access is based on user's role in the organisation
- The administrator associates various permissions to each role
- Each user is assigned at least one role and inherits the permissions associated to the role(s)
	![[Pasted image 20250424153537.png]]

#### The Intuition Behind RBAC:
- Abstraction: 
	- Many subjects (or objects) have identical attributes, and a policy is based on these attributes
- Hierarchy: 
	- Often functional/organisational hierarchies that determine access rights
- RBAC uses the notion of "role" as the central authorisation method
	- A role is an abstract representation of a group of subjects that are allowed to perform the same operations on the same subjects
	- The objects (i.e. accessible shared data) in the system are assigned to an authorised role 
	- The subjects (i.e. users) need to identify themselves to acquire these roles to access and operate on the objects

#### Advantages of RBAC
- Roles are abstraction of jobs or functions in an organisation
	- Distinct from notion of user groups, which names collections of users
	- Emphasis is on responsibility and associated permissions
	- Widely used by companies
- Increases abstraction in policies
- Policies become more manageable
- Reduces user administration
- Easy to audit
- Higher flexibility and scalability 

#### RBAC Family:
- Base model is the original RBAC:
- Role hierarchies enable one role to inherit permissions from another role
- Constraints restrict the ways in which the components of an RBAC may be configured
- Consolidates model combines role hierarchies and constraints 
	![[Pasted image 20250424160341.png]]

#### RBAC - Role Hierarchies:
- Roles above other roles can access all objects from the roles below it

#### RBAC - Constraints:
- A constraint is a defined relationship among roles or a condition related to roles
- Mutually exclusive roles:
	- A user can be assigned to only one role
		- Support a separation of duties and capabilities within an organisation
	- Any permission can be granted to only one role 
		- Increase the difficulty of collusion or divergent job functions to thwart security policies
- Cardinality:
	- Setting a maximum number with respect to roles 
		- A risk mitigation technique for a sensitive or powerful permission 
- Prerequisite roles
	- A user can only be assigned to a particular role if it is already assigned to some other specified role(s)

#### Attributes:
- Attributes are characteristics that define specific aspects of the subject, object, environment conditions, and/or requested operations
- Subject attributes define the identify and characteristics of the subject
	- E.g. identifier, name, organisation and job title
- Object attributes can often be extracted from the metadata of the object
	- E.g. title, subject, date, author and service taxonomy
- Environment attributes describe the operational, technical and even situational environment or context in which the information access occurs
	- E.g. current date and time, current virus/hacker activities, network's security level

#### Attribute-Based Access Control (ABAC):
- Access control by evaluating rules against the attributes of entities (subject and objects), operations, and the environment relevant to a request
- A streaming service control access to a content based on age of user & rating of the content
	- E.g. children under 13 will not be allowed to watch contents with PG-13 and R
	- Check the age of the subject and the rating of the content
- Now, the streaming service introduces a premium service, where customers can watch new releases
	- Check the subscription of the subject

#### Advantages and Disadvantage
- Dynamic: Access control is evaluated at the time of the actual request is made
- Contextual: Environment conditions can be considered
- Fine-grained: Providing a bigger set of possible combinations of attributes to reflect a larger and more definitive set of rules, policies, or restrictions on access
	- Can enforce DAC, MAC and RBAC concepts
- Complexity of the design and implementation, in terms of the performance impact, is likely to exceed that of other access control model

#### Other Access Control Models:
- Models can capture policies for confidentiality or for integrity
- Some models apply to environments with static policies, others consider dynamic changes of access rights
- Security models can be informal, semi-formal, or formal

# References