03-02-2025 14:43

Status:

Tags: [[Algorithmics]] [[Data Structures]]


# Links

#### Arrays:
- An array uses a contiguous chunk of memory
- It has access time of $\Theta(1)$
	- The constant factor is small
- Arrays provide a very efficient use of memory
- 95% of the time using arrays is going to give the best performance
- Disadvantages:
	- fixed length (but can use variable-length arrays, at extra cost)
	- insertion/deletion to/from the middle have $\Theta(n)$ time complexity

#### Variable-Length Arrays: Time Analysis:
- Most add(elem) operations are $\Theta(1)$ 
- When we are at full capacity we have to copy all elements
- How efficient is resizing?
- Adding to a full array is slow but this is amortised by other quick adds

#### Example:
- If we have an initial capacity of 10 and add 100 elements, doubling the array size whenever required, then the number of operations needed is
	- adds: 100
	- copies: 10+20+40+80
	- new int[]:4
- 250 add and copy operations + 4 new operations

#### General Time Analysis:
- If we perform $N$ adds with an initial capacity of $n$
- We must perform $m$ copies where:
![[Pasted image 20250204100722.png]]
- The number of elements copied is:
![[Pasted image 20250204100753.png]]

![[Pasted image 20250204100856.png]]

- The amortised cost of add(elem) is thus $\Theta(1)$!

#### Non-Contiguous Data:
- Storing data in a contiguous 


#### Self-Referential Classes:
- The building block for a linked list is a node:
	![[Pasted image 20250204101443.png]]
- This contains a reference to another node object
    ![[Pasted image 20250204101517.png]]



# References