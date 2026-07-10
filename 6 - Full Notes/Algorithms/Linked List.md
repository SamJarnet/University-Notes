04-02-2025 10:13

Status:

Tags: [[Algorithmics]] [[Data Structures]] [[Links]]


# Linked List

#### Singly-Linked List:
- We can build a linked list by stringing nodes together:
	![[Pasted image 20250204101600.png]]
	- We don't show the "pointer" to element
- A singly linked list has a single "pointer" to the next node
- A doubly linked list has "pointers" to the next and previous node
- We should be able to create a linked list, add elements, remove elements, see if an element exists, etc.

#### Java Implementation:
- We consider a lightweight implementation
- The class will have a head, a size counter and have Node as a nested class:
	![[Pasted image 20250204101803.png]]

#### Simple Methods:
- The constructor is simple (and not strictly necessary)
	![[Pasted image 20250204101851.png]]
- Other simple methods are:
	![[Pasted image 20250204101912.png]]

#### Adding Elements:
![[Pasted image 20250204101941.png]]



#### Removing the List Head:
![[Pasted image 20250204102222.png]]

#### Contains:
- Does the list contain obj?
	![[Pasted image 20250204102257.png]]
- current iterates over nodes in list
- end when current == null 
- All classes have equals method

#### Other Methods:
- We can easily implement many other methods:
	- get_head() - returns element at head of list
	- get(int i) - returns the $i^{th}$  item in list
	- remove(T obj) - remove obj from list
- Note that get(int i) requires moving down the list so is $\Theta(n)$ (i.e. not random access) both in worst case and in average case
- remove (T obj) is also $\Theta(n)$

#### Stack Implementation:
![[Pasted image 20250204102822.png]]


#### Complexity of Stack Implementation:
- All stack operations take constant time, i.e. $\Theta(1)$ 
	- hidden cost of creating and destroying Node objects
- Memory requirement is $\Theta(n)$
	- approximately $2\times n$ references and $n$ objects
- An array implementation is therefore better in practice

#### Point to the Back:
- To find the end of the list takes $n$ jumps
- Thus our linked list isn't the right data structure to implement a queue
- However, we could include a pointer to the end of the list
	![[Pasted image 20250204103106.png]]


#### Implementing a Queue:
- We can then add elements to the tail in constant time
- We can then implement a queue in $\Theta(1)$ time by
	- enqueueing at the back
	- dequeuing at the head
- Note that although adding an element to the tail is constant time, remove an element from the tail is $\Theta(n)$ as we have to find the new tail

#### Doubly Linked List:
- Java provides a linked list class $LinkedList<T>$ which allows $\Theta(1)$ add and remove at both ends of the list
- To achieve this it uses a doubly-linked list with pointers to the next and previous nodes
	![[Pasted image 20250204103510.png]]

#### Dummy Node:
- Dummy node used to make implementation slicker
	![[Pasted image 20250204103542.png]]
- Symmetric data structure so processing head and tail is equally efficient


#### Time Complexity:
- add and remove from head and tail is $\Theta(1)$ 
- find $O(n)$ and slow 
- insert and delete $\Theta(1)$ (faster than an array list) once position is found
	![[Pasted image 20250204103827.png]]

#### They are a bit shit
- Cant do much

#### Line Editor:
- One application where 




# References