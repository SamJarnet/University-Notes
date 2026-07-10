28-01-2025 10:13

Status:

Tags: [[Algorithmics]]


# Time Complexity

#### Sorting:
- A very common problem, we care about solve time
- Comparison between common algorithms:
	- Insertion sort - easy to code
	- Shell sort - invented in 1959
	- Quick sort - invented in 1961
- These numbers take a list of numbers and returns a sorted list
- You only really care about large inputs
- We would like to analyse/quantify the performance of an algorithm without running them

#### Input size:
- The running time of an algorithm depends on the size of its input
- How do we measure input size?
	- Number of elements, in sorting
	- Number of bits, in integer multiplication
	- Number of nodes/edges, in a graph problem
	- ...
- It is problem dependent


#### Running time:
- We want to estimate the running time of algorithms:
	- This depends on implementation, the compiler, the hardware
	- We want to abstract away differences in implementations, compilers, hardware!
- We will take the running time of an algorithm on a given input to be the number of "steps", or primitive operations (e.g. addition, comparison, assignment) executed
	- all primitive operations take ~~ the same amount of time
	- so counting primitive operations gives a good measure of the time taken by the algorithm, up to a constant factor
	- we can then assign a cost to each line of pseudocode in our algorithm by counting primitive operations

#### Example:
![[Pasted image 20250128102821.png]]
- $C_i$ counts the primitive operations in line $i$
- For each array of size $n$, the algorithm takes:
	- $T(n) = C_1 + C_2 + C_2 \times n + (c_4 + c_5) \times (n-1)$
	 primitive operations
- Thus $T(n) = a \times n + b$ with $a$ $b$, constants
	- $T(n)$ only depends on the array size and not the specific input
 - Line 4.1 is only executed sometimes!
 - the number of steps now depends on the actual array!
 - best case: minimum value in first position
 - worse case: array values in decreasing order

#### Time complexity (Running Time) of an Algorithm:
- In general, the running time depends not only on the input size but the input itself
	- for a fixed case, there is a best case and worst case!
- The worst-case running time (time complexity) of an algorithm is a function $T : \N \rightarrow \N$ where:
	- $T(n)$ is the maximum number of primitive operations the algorithm uses on inputs size $n$
- This gives a guarantee that the algorithm will not take longer
- The average-case running time (time complexity) is similar: replace maximum by average
	- Note this assumes that all inputs are equally likely
	- A more general definition assumes distribution over inputs

#### Example:
![[Pasted image 20250128103329.png]]
- hence the worst-case and the average-case running time is:
	- $T(n) = (c_3 + c_4 + c_5) \times n + (c_1 + c_2 - c_4 - c_5)$ 

![[Pasted image 20250128120041.png]]
- the worst-case running time is as before
	- in the worst case, the values are in decreasing order
- the average-case running time is slightly lower...
	- ... but still roughly proportional to $n$

#### Rate of Growth of the Running Time:
- Suppose we have an algorithm that takes $4n^2 + 12n + 199$ primitive operations in the worst case
- We are interested in what happens when $n$ becomes very large
	- This is called asymptotic behaviour of the running time
- For large $n$ we have $4n^2 >> 12n + 100$ 
	- we can ignore the $12n + 199$ part as it is dominated by $4n^2$
	- we only consider the leading term, namely $4n^2$
- For large $n$, the constant within the leading term is not that significant either
	- We can ignore the constant 4
	- we only take the functional behaviour, namely $n^2$ 
- Key observation: $4n^2 + 12n + 199$ grows at the same rate as $n^2$

#### Big-Theta Notation:
- Let $f,g : \mathbb{N} \rightarrow \mathbb{R}^{+}$ 
- $f(n)$ is $\Theta(g(n))$ if there exist constants $c>0, d>0$ and $N \in \mathbb{N}$ such that:
	- $cg(n) \leq f(n) \leq dg(n)$ for $n \geq \mathbb{n}$ 
- The $\Theta$ notation captures the idea that two functions have the same rate of growth

#### Example:
![[Pasted image 20250128121045.png]]

#### Advantage of the Big-Theta Notation:
- We can compare algorithms by comparing the rates of growth of the running times:
	- e.g. a $\Theta(n^2)$ algorithm will always be better than a $\Theta(n^3)$ algorithm for large enough $n$ 
- We can estimate algorithm running times on large inputs by measuring running time on a small input:
	- If $T(n) $ roughly $cn^2$ for $n >> 1$, for some $c>0$
	- If it takes $x$ seconds on average on input size of 100
	- It will take about $(x\times n^2)/100^2$ seconds on average of an input of size $n$
#### Disadvantages of Big-Theta Notation:
- Can not compare algorithms whose running times have the same rate of growth!
- For small inputs Big-Theta can be misleading. E.g.
	- algorithm A takes $n^3 + 2n^2 +5$ operations
	- algorithm B takes $20n^2 + 100$ operations
	- algorithm A is $\Theta(n^3)$ and algorithm B is $\Theta(n^2)$ 
	- algorithm A is faster than algorithm B for $n <18$ 
	- But who cares? Asymptotically, a $\Theta(n^2)$ will always be faster than a $\Theta(n^3)$ algorithm, even when they run on different machines!

#### Counting Operations:
- The rate of growth of the running time of an algorithm is often easy to calculate
![[Pasted image 20250128121854.png]]

- For the above algorithms, assuming no if statements or other loops, the average-case and worst-case running times coincide
	-  The number of primitive operations executed only depends on the size of the input! 

#### Not so Sure:
![[Pasted image 20250128122027.png]]
- The rate of growth of the running time now depends on the if statement, and is much harder to analyse...
- ... but will be somewhere between $\Theta(n)$ and $\Theta(n^2)$ 


#### Bounds:
- To avoid having to think really hard we can look for upper and lower bounds for the rate of growth functions (e.g. running times)
- Can use Big-O notation to give upper bound for rate of growth:
	- The running time of the previous algorithm is $O(n^2)$ 
	- i.e. it executes no more than order $n^2$ operations
	- this is true for either worst/average/best case!
- Can use Big-Omega notation to give lower bound for rate of growth:
	- The running time of the previous algorithm is $\Omega(n)$
	- i.e. it executes no less than order $n$ operations
	- this is true for either best/average/worst case!

#### Bounding Running Times:
- When we are given an algorithm to analyse, we want to find the rate of growth of $T(n)$ ($T(n)$ can be the average/worst/best-case running time !)
- This may be difficult; however, it is often easy to find bounds
![[Pasted image 20250128122642.png]]

#### Big-O and Big-Omega Notations:
![[Pasted image 20250128122727.png]]


#### Big-O notation:
![[Pasted image 20250128122753.png]]


#### Use and Misuse:
- Big-O notation is most commonly used
- Often people say that they have a $O(n^2)$ algorithm when in fact they have a $\Theta(n^2)$ algorithm (a stronger statement)
- Any $O(n^2)$ algorithm is also a $O(n^3)$ algorithm
- A $O(n^2)$ algorithm may not be faster than a $O(n^3)$ algorithm for large $n$ 
- Big-O, Big-Theta and Big-Omega notation can be used to describe any of worst-case, average-case or best-case running times

#### Insertion Sort: Best and Worst Case:
![[Pasted image 20250128123347.png]]
- worst-case: array values are strictly decreasing
- best case: array is already sorted
- worst-case running time is $\Theta(n^2)$ 
- best-case running time is $\Theta(n)$ 





# References