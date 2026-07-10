03-02-2025 14:24

Status:

Tags: [[Algorithmics]] [[Data Structures]]


# Queues

#### Queues:
- First-In-First-Out (FIFO memory model
- enqueue(T elem)
- T peek()
- T dequeue()
- boolean isEmpty()

#### Implementation of Queues:
- Either using arrays or using linked lists
- Java has a $Queue<T>$ interface with all the wrong names
	- add(elem) or offer(elem) instead of enqueue
	- remove() or poll() instead of dequeue
	- element() and peek() to peek
- It also has
	- Double ended queues, Dequeue (allow add/remove at both ends)
	- BlockingQueue and BlockingDeque that support concurrency

#### Uses of Queues:
- In operating systems
	- print queues
	- job queues
- Communication/message passing

#### Priority Queues:
- Queue with priorities
- insert(T elem, int priority)
- T findMin()
- T deleteMin()

#### Uses of Priority Queues:
- Operating systems
- Greedy algorithms
	- Prim's minimum spanning tree algorithm

#### Implementation of Priority Queues:
- Could be implemented using a [[Linked List]] or a [[Binary Tree]]
- Most efficient implementation uses a heap (binary tree implemented using an array)




# References