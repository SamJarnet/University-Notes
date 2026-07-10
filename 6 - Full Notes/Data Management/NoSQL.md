29-12-2024 17:53

Status:

Tags: [[Data Management]] [[SQL]] [[Database Systems]]


# NoSQL

#### Benefits of NoSQL:
- Simplicity of the Model:
	- It does not require any complex queries because it has no query processing or structuring so simple SQL queries are enough to handle
- Ease of Use:
	- Users can easily access/retrieve their required information within seconds without indulging into complexity of the database. SQL is used to execute the complex queries of the users
- Accuracy:
	- A key feature of relational databases is that they're strictly defined and well-organised, so that data doesn't get duplicated. Relational databases have accuracy because of their structure with no data duplication
- Data integrity:
	- RDBMS databases are also widely used for data integrity as they provide consistency across all tables. The data integrity ensures the features like accuracy and ease of use
- Normalisation:
	- Database normalisation ensures that a relational database has no variety or variance in its structure and can be manipulated accurately. This ensures that integrity is maintained when using data from this database for your business decisions
- Collaboration:
	- Multiple users can access the database to retrieve information at the same time and even if data is being updated
- Security:
	- Data is secure as Relation Database Management System allows only authorised users to directly access the data. No authorised user can access the information


#### Requirements and Constraints:
 - Schema design:
	 - Relational databases require a predefined schema, which can be challenging to design for complex and evolving data structures such as those found in health, imaging, or generic data. 
 - Performance:
	 - Relational databases can handle large volumes of data, their performance usually degrades as the dataset grows, especially for complex queries involving joins or aggregations across multiple tables
- Data Integrity:
	- Relational databases excel at enforcing data integrity constraints through features like foreign keys and transactions. This ensures consistency and accuracy of the data stored in the database. For certain types of data, strict relational integrity may not be necessary or may even be impractical
- Scalability: 
	- Relational databases can scale vertically by upgrading hardware resources (CPU, memory, storage), but they may face limitations in horizontal scalability, especially for distributed architectures or massively parallel processing.
- Storage Efficiency: 
	- Storing large binary data such as imaging data in relational databases can be inefficient, as they are typically stored as BLOBs (Binary Large Objects) or as references to external files. This can impact storage efficiency and retrieval performance, especially for large-scale biobanks with terabytes or petabytes of data.


#### NoSQL?
- It doesn't mean NO SQL
	- It means Not Only SQL
	- It is possible to use SQL or SQL-like languages with NoSQL databases
- It means being rebellious
	- Not conforming to the Relational Database Management System (RDBMS) traditions and conventions!
		- Less strict adherence to ACID
		- Less script adherence to schemas
	- A break away from relations
- There are various different approaches
- The aim: Scalability, availability, performance, simplicity!
	- But at a cost to consistency


#### Detailed Definition:
- NoSQL database is a type of database that provides a mechanism for storage and retrieval of data that is modelled in a non-tabular format.
- Unlike traditional relation databases, which are typically based on SQL (Structured Query Language) and have a rigid schema, NoSQL databases are more flexible and can handle various types of data.
- NoSQL databases are designed to handle large volumes of data and often used in applications where scalability, high availability, and flexibility are key requirements. They are particularly well-suited for use cases such as web applications, real-time analytics, and handling big data.

#### Rigid Schema in Relational Databases:
- Relational database rely on SQL (Structure Query Language) and enforce a rigid schema. This means:
	- The structure of the data (e.g. tables, columns, data types) must be predefined
	- All data entries must adhere strictly to this schema
	- Any changes to the schema, such as adding or removing columns, require careful planning and often downtime, as the database structure needs to be updated

- This rigidity makes relational databases ideal for applications with consistent, predictable data, such as:
	- Financial systems (e.g. banking transactions)
	- Enterprise resource planning (ERP)
	- Inventory management

- However, these limitations can make it challenging to handle:
	- Evolving data structures
	- Large-scale, heterogenous datasets
	- High-volume, real-time data


#### Flexibility of NoSQL Databases:
- Schema-less or Dynamic Schemas:
	- NoSQL databases do not require a fixed schema. Data can stored without predefining its structure
	- For example, in a document-based NoSQL database MongoDB, one document in a collection can have fields that others do not, or fields can hold different types of data
	- This flexibility is particularly useful for rapidly evolving applications where data requirements change flexibility
- Support for Diverse Data Types:
	- Structured Data: 
		- Highly organised data, such as rows and columns in a table
	- Semi-structured data: 
		- Data that does not conform to a fixed schema but still has some organisational properties, such as JSON or XML files
	- Unstructured data:
		- Data without a defined format, such as text, images, videos and sensor data

#### Distribution is key to performance:
- Scalability refers to the ability of a system to handle increasing amounts of workload or data by adding resources to the system. In the context of databases, scalability typically refers to the ability to handle more data, more users, or more requests without sacrificing performance or availability


#### Vertical Scalability (Scaling Up):
- Involves increasing the capacity of a single database server by adding more powerful  hardware such as:
	- More CPU power
	- Increased memory (RAM)
	- Faster storage (e.g. SSDs)
- Advantages:
	- Simple to implement
	- Requires few architectural changes
- Limitations:
	- Hardware upgrades have a cost limit
	- A single point of failure may persist 


#### Horizontal Scalability (Scaling Out):
- Involves adding more servers or instances to distribute the workload across multiple machines
- Achieved through:
	- Sharding (splitting the database into smaller, more manageable parts)
	- Replication (creating copies of the database for load distribution)
- Advantages:
	- Nearly unlimited scalability potential
	- Improved fault tolerance and redundancy
- Challenges:
	- Requires careful design to ensure consistent data and efficient query handling
	- Complexity increases with more distributed nodes

#### Distribution is key to performance:
- Distributed Architectures:
	- NoSQL databases are designed to operate in distributed environments, where nodes communicated with each other over a network.
	- Distributed architectures provide resilience against failures and enable linear scalability, meaning that adding more nodes the cluster increases its capacity proportionally
- Sharding: 
	- Sharding involves partitioning data across multiple nodes in a distributed system.
	- Each node (or shard) is responsible for a subset of the data. By distributing data in this way, NoSQL databases can distribute the workload evenly across nodes, allowing them to handle more data and requests in parallel
- Replication:
	- Replication involves maintaining copies of data across different nodes in a cluster.
	- Replication provides fault tolerance and high availability, as data can still be accessed even if some nodes fail. 
	- Additionally, replication can improve read performance by allowing clients to read from replication by allowing clients to read from replicas located closer to them

#### [[CAP Theorem]]

#### Key-Value:
- A key-value database is a type of NoSQL database that stores data as a collection of key-value pairs. In this model, each data item (or value) in the database is associated with a unique key, which can be used to retrieve the data when needed.
- Key-value databases are highly efficient for simple read and write operations because they offer very fast access to data based on the key. This simplicity and efficiency make them suitable for a wide range of use cases, especially those requiring high-speed data retrieval and low-latency access.


#### Characteristics of key-value databases:
- Simple data model: 
	- Key-value databases have a straightforward data model where each data item is stored with a unique key. There is typically no schema or structure enforced on the data, allowing for flexibility in storing different types of data
- High-performance:
	- Key-value databases are optimised for fast read and write operations. They often achieve high performance by using in-memory caching, asynchronous replication and other optimisation techniques 
- Scalability:
	- Many key-value databases are designed to scale horizontally, allowing them to handle large amounts volumes of data and high traffic loads. They can distribute data across multiple nodes in a cluster to support growing workloads
- Flexible Data Types: 
	- Key-Value databases can store various types of data, including strings, integers, binary data, and more complex data structures like JSON objects.
- Use Cases:
	- Key-value databases are commonly used in applications that require fast and efficient data access, such as caching, session management, user profiles, real-time analytics and distributed systems


#### DOCUMENT:
- Data Model:
	- Data is stored in documents, typically in JSON, BSON or XML formats. Each document contains key-value pairs and can include nested structures/
- Schema:
	- Schema-less or dynamic schema, allowing different documents in the same collection to have different structures
- Use cases:
	- Content management systems
	- User profiles
	- E-Commerce product catalogues
- Advantages: 
	- Highly flexible for semi-structured data
	- Supports hierarchical relationships (e.g. nested fields)
	- Easy to scale horizontally
- Examples:
	- MongoDB
	- Couchbase

#### COLUMN-Family:
- Data model:
	- Data is stored in rows and columns, but unlike relational databases, the columns in a row can vary. A column family groups related columns together
- Schema:
	- Semi-structured; each row can have different columns
- Use cases:
	- Time-series data
	- Real-time analytics
	- IoT sensor data
- Advantages:
	- Optimised for write-heavy applications
	- Supports large-scale distributed systems
- Examples:
	- Apache Cassandra
	- Apache HBase

#### Graph:
- Data Model:
	- Data is stored as nodes, edges and properties, making it ideal for representing relationships and interconnected data
- Schema:
	- Flexible schema; nodes and edges can have different properties
- Use cases:
	- Social networks
	- Recommendation systems
	- Fraud detection
- Advantages:
	- Designed for complex queries involving relationships 
	- Efficient for traversing data (e.g. finding shortest paths)
- Examples:
	- Neo4j
	- Amazon Neptune



#### Hybrid NoSQL Databases
- Hybrid NoSQL databases are systems that combine features from multiple types of NoSQL databases, offering flexibility to handle diverse data models and use cases within a single database solution. They aim to provide the best of multiple NoSQL paradigms to meet complex application requirements.













# References