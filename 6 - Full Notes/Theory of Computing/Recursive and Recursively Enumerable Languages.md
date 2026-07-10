2025-11-09 20:29

Status:

Tags: [[Theory of Computing]] [[Turing Machines]]


# Recursive and Recursively Enumerable Languages

#### Total Turing Machines
- A TM $M$ is said to halt on input $x$ if it either accepts or rejects $x$
- It is possible that a machine neither rejects nor accepts an input $x$: the machine loops on $x$
- A TM is said to be total if it halts on all inputs 
- Let $L(M)$ be the set of strings accepted by a TM $M$: $L(M)$ is the language of $M$
- A set $X$ of strings is called
	- Recursively enumerable if $X = L(M)$ for some TM $M$
	- Co-recursively enumerable if its complement is recursively enumerable.
	- Recursive if $X = L(M)$ for some total TM $M$ 

#### Example 1
- Set:
	- $\{ww | w \in \{a, b\}^*\}$
- Is recursive, i.e. accepted by total TM
- Corresponding TM $M$ works as follows:
	- If it is, $M$ writes $⊣$ and repeatedly scans back and forth over input
	- At each right-to-left pass, it marks first unmarked $a$ or $b$ with $´$
	- At each left-to-right pass, it marks first unmarked $a$ or $b$ with $`$
	- $M$ machine continues until all symbols are marked

- Formally, marking symbols  means replacing them i.e.:
	- ![[Pasted image 20251110191121.png]]
- Suppose input is $aabbaaabba$, marking proceeds as follows:
	- ![[Pasted image 20251110191202.png]]
- This allows us to find centre of string

- Now $M$ scans left to right.
	- ![[Pasted image 20251110191242.png]]
- $M$ erases first symbol marked with $`$ and remembers it in its finite control
- $M$ scans forward until finds symbol marked with ´, checks it is the same, and erases it, if it is not it rejects
- When $M$ has erased all symbols, it accepts
	- ![[Pasted image 20251110191420.png]]

#### Recursive and Recursively Enumerable Sets
- A set $A$ is recursively enumerable if it coincides with the language of a TM
- A set $A$ is recursive if it coincides with the language of a total TM
- Recursive sets are closed under complement i.e.:
	- if $A$ is recursive, so is $A^c = \Sigma ^*$ \ $A$ 
- Suppose $A$ is recursive, then there exists a total TM such that:
	- $A = L(M)$
- Switch accept and reject states of $M$, and obtain total machine $M'$ 
- Consequently:
	- $A^c = L(M')$

- Above construction works because recursive sets are accepted by total machines
- "Rejecting" and "not accepting" are not synonymous for non-total machines
- If $A$ is recursively enumerable, then there exists some TM $M$ that accepts all its strings
- $A^c$ contains strings rejected by $M$ but also the strings where $M$ loops (if any)
- So, switching accept and reject states for a non-total machine does not work the same as for recursive languages
- Every recursive set is recursively enumerable, but not vice versa, i.e. not every TM is equivalent to a total one
#### Proof
- Proposition:
	- If a set $A$ and its complement $A^c$ are recursively enumerable, then $A$ is recursive
- Proof:
	- We prove this by building a total TM $N$ for $A$ 
	- Let $M, M'$ be such that:
		- $A = L(M), A^c = L(M)$ 
	- Build TM $N$ that on input $x$ runs both $M$ and $M'$ simultaneously
	- Formally tape alphabet of $N$ contains symbols of the form:
		- ![[Pasted image 20251110192454.png]]
	- Where $a$ is tape symbol of $M$ and $c$ is tape symbol of $M'$ 
	- Each cell represents two cells, one with $M$ and one with $M'$ 
	- Marks ^ are placed on tape to indicate current positions of simulated heads of $M$ and $M'$ 
	- On input $x_1,...,x_k$, $N$ rewrites non empty portion of the tape as follows:
		- ![[Pasted image 20251110193244.png]]
	- Then $N$ performs the following loop:
		- 1. Scans the tape to find a symbol with a hat in the "upper" section of the tape. Then, according to the transitions of $M$, it performs $M$'s move
		- 2. If $M$ accepts, then $N$ accepts
		- 3. Scans the tape to find a symbol with a hat in the "upper" section of the tape. Then, according to the transitions of $M'$, it performs $M'$'s move
		- 4. If $M'$ accepts then $N$ rejects. 
	- Any $x$ either belongs to $A$ or $A^c$, so it is accepted by either $M$ or $M'$ 
	- By construction $x$ will either be accepted or rejected by $N$
	- So, $N$ is total, and $A$ is recursive

#### Decidability and Semidecidability
- Let $P$ be a property of strings, i.e. for any $x \in \Sigma ^*$ 
	- Either $P(x)$ or $¬P(x)$
- For instance "has length 2"
- $P$ is decidable iff $\{x \in \Sigma^*| P(x)\}$ is recursive
- $P$ is semidecidable iff $\{x \in \Sigma^*| P(x)\}$ is recursively enumerable
- Decidability and semidecidability are applied to properties
- Recursive and recursively enumerable are applied to sets 
- A set $A$ is recursive iff "$x \in A$" is decidable
- A set $A$ is recursively enumerable iff "$x \in A$" is semidecidable
 

# References