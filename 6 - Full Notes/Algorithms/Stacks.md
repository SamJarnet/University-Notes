03-02-2025 14:08

Status:

Tags: [[Algorithmics]] [[Data Structures]]


# Stacks

#### Stacks:
- Last In First Out (LIFO) memory
- Standard operations:
	- push(T item)
	- T peek()
	- T pop()
	- boolean isEmpty()
- Implemented using an array or a linked list

#### Array Implementation of Stacks
- stack of at most $n$ elements using array $S[1..n]$ 
- $top$ indexes most recently added element (initially 0) 
![[Pasted image 20250203141256.png]]
- Complexity of Stack operations:
	- all have $\Theta(1)$ complexity!

#### Why use a stack?
- Gives you a very simple interface
- Reduces the access to memory - no longer random access!
	- Seems counter intuitive to limit what you can do
	- But prevents another programmer from using memory in a way that may break existing code
- Sufficient for many applications 

#### Uses of Stacks:
- Reversing an array
- Parsing expressions for compilers
	- balancing parentheses
	- matching XML tags
- Evaluating (arithmetic) expressions

#### Evaluating Arithmetic Expressions: ![[Pasted image 20250203141826.png]]
- Thus, evaluating arithmetic expressions is $O(n)$ (where $n$ is the size of the expression)

#### Java Stacks (or How Not To Do Stacks):
- In Java the class $Stack<T>$ implements push, pop, peek, empty and search
- Search extends the Vector class
	- a stack isn't a type of vector - it could be implemented by a Vector but it should not extend Vector!




# References