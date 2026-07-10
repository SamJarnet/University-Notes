30-12-2024 21:15

Status:

Tags: [[Data Management]]


# CAP Theorem


#### The CAP theorem:
 Also known as Brewer's theorem, states that it is impossible for a distributed data system to simultaneously guarantee all three of the following properties:
	- Consistency:
		- Every read receives the most recent write or an error
	- Availability:
		- Every request receives a response without guaranteeing that it contains the most recent write
	- Partition Tolerance:
		- The system continues to operate despite network partitions (communication failures) that may cause some parts of the system to be unavailable or isolated from each other

#### Trade-offs of CAP theorem:
- CP (Consistency and Partition Tolerance):
	- Systems that prioritise consistency and partition tolerance aim to maintain strong consistency even in the face of network partitions
	- In a CP system, if a network partition occurs, the system sacrifices availability to ensure that all nodes have consistent and up-to-date data
	- Examples of CP systems include relational databases and systems that prioritise data integrity and correctness over availability
- AP (Availability and Partition Tolerance):
	- Systems that prioritise availability and partition tolerance aim to remain operational and responsive to client requests, even if the presence of network partitions
	- If an AP system, if a network partition occurs, the system sacrifices consistency to ensure that it remains available to serve requests
	- Examples of AP systems include NoSQL databases and systems that prioritise high availability and responsiveness over strong consistency


#### CA (Consistency and Availability):
- CA, without Partition Tolerance, is theoretically possible in a single-node system or in a partition-free environment. However, sacrificing partition tolerance is not a viable option in a distributed system where network partitions are inevitable. In a CA system:
	-  Consistency (C): The system ensures that all nodes have the same data at the same time. When a client reads data from any node, it receives the most  recent and up-to-date version of that data. Updates to the data are immediately visible to all clients
	- Availability (A): The system remains operational and responsive to client requests, providing a response (either success or failure) within a reasonable time frame. Even in the absence of network partitions or node failures, the system continues to function and serve requests.
- However, achieving both strong consistency and high availability without partition tolerance is challenging in a distributed environment. Network partitions can occur due to various factors, such as network failures, hardware failures, or software issues
- Therefore, while CA may be achievable in certain scenarios, such as single-node systems or partition free environments, it is not practical or feasible for distributed systems where partition tolerance is essential for ensuring resilience and fault tolerance


#### ACID vs BASE:
- In NoSQL databases, the Atomicity, Consistency, Isolation, and Durability (ACID) properties are often relaxed in favour of achieving other desirable characteristics such as scalability, availability, and partition tolerance. NoSQL databases typically prioritise availability and partition tolerance over strict consistency. 

![[Pasted image 20241230210655.png]]

- Basically Available:
	- The system guarantees availability, meaning the database will always respond to a request, even if it cannot guarantee the most recent data is being served
	- It prioritises availability over strict consistency, making it suitable for distributed systems where downtime must be minimised
	- (The database will always be available to provide an answer)
- Soft State:
	- The state of the database may change over time, even without new input due to eventual consistency.
	- This reflects a system that allows for temporary inconsistencies as data is being replicated and synchronised across nodes.
	- (The state of the system may change without user input to achieve eventual consistency)
- Eventual Consistency:
	- The system does not guarantee immediate consistency across all nodes after a write operation
	- Instead, it ensures that if no new updates are made, all nodes will eventually converge to the same state
	- (At some point, database will be consistent)




# References