03-02-2025 14:41

Status:

Tags: [[Algorithmics]] [[Data Structures]]


# Maps

#### Maps:
- A map provides a content addressable memory for pairs $key:data$
- It provides fast access to the data through the key
	- no duplicate keys!
- Operations:
	- put (K key, V value)
	- V get (K key)
	- V remove (K key)
	- int size()
- Implemented using binary trees or hash tables
- Multimaps allow each key to be associated with multiple values

#### Program to Interfaces not Implementations:
- Using data structures through their interfaces (ADT)
	- ![[Pasted image 20250203150018.png]]
- Much better than
	- ![[Pasted image 20250203150037.png]]
	- which is implementation dependent and can make modification and maintenance hard
- Declare your intentions, not your actions 
- Program to interfaces, not implementations





# References