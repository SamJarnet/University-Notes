02-11-2024 17:34

Status:

Tags: [[Mathematics I]] [[Sets]]


# Infinite Sets

#### Sizes of infinity:
- If X and Y are finite sets. Suppose that $f: X \rightarrow Y$ is a function:
	- If is injective: $∣X∣ ≤ ∣Y∣$
	- If f is surjective: $|X∣ ≥ ∣Y∣$
	- If f is bijective: $∣X∣ = ∣Y∣$

- We have seen that the following three conditions are equivalent for finite sets X and Y
	- X and Y have the same cardinality
	- there is a bijection (1-1 correspondence) $f:X \rightarrow Y$
	- there is an invertible function $f: X \rightarrow Y$ 

- Generalise concept of cardinality to all sets as follows:
	- $|X| = |Y|$ whenever there exists a bijection $f: X \rightarrow Y$
	- Not always the case for infinite sets

- For finite sets $X \subset Y$ implies $|X| < |Y|$. This is not the case for infinite sets

- ![natural numbers - proving that f:N^2->N is bijective - Mathematics Stack  Exchange|400](https://i.sstatic.net/LZACv.png)

#### Countable sets:
- A set X is called countable if there exists a bijection $f:\mathbb{N} \rightarrow X$ where $\mathbb{N}$ is the set of all natural numbers.
- Examples of countable sets:
	- {1, 2, 3, …}
	- $\mathbb{Z}$ = {... -2, -1, 0, 1, 2, …}  
	- $\mathbb{N} \times \mathbb{N}$
	- $\mathbb{Q}$ (the rationals)

#### The size of the continuum:
- $(0, 1) = \{x \in \mathbb{R} \, | \, 0<x<1 \}$,  Clearly $(0, 1) \subset \mathbb{R}$ 
- But surprisingly, (0, 1) and $\mathbb{R}$ have the same cardinality!

#### Uncountable sets:
- Theorem: The set of real numbers $\mathbb{R}$ is not a countable set
- Proof (Diagonalisation): We will prove the following:
	- There are no surjective functions $f : \mathbb{N} \rightarrow \mathbb{R}$
	- There is enough to prove the theorem

#### Diagonalisation:
 First define a function $\_ : \{0, ..., 9\} \rightarrow \{0, ..., 9\}$
- instead of $\_(x)$ we will write $\underline{x}$
- let $\underline{0}, \underline{1}, \underline{3}, \underline{4}, \underline{5}, \underline{6}, \underline{7}, \underline{8}, \underline{9} = 5$
- and $\underline{5} = 6$
- The actual definition is not so important, the important part is that it has no fixed point i.e. there is no x such that f(x) = x

Suppose that $f:\mathbb{N} \rightarrow \mathbb{R}$ is some function. For simplicity (and without loss of generality) we will assume (0, 1) instead of $\mathbb{R}$:

![[Pasted image 20241102212816.png]]

- 0 . x0,0 x1,1 x2,2 x3,3 x4,4 x5,5 x6 doesn't appear in the list so there are more numbers that can e created so the cardinalities of $\mathbb{N}$ and $\mathbb{R}$ are different
- There is the obvious injective function $\mathbb{N} \rightarrow \mathbb{R}$ that sends a natural number to itself, thought of as a real
- Are there any injective functions $\mathbb{R} \rightarrow \mathbb{N}$? No.
	- injections give rise to an ordering between cardinalities
- In this sense $\mathbb{R}$ can be said to have a larger cardinality than $\mathbb{N}$

#### Cantor’s Theorem

-  For any set X, the cardinality of P(X) is strictly greater.

#### Cantor-Bernstein-Schröder Theorem

-   If there exist injective functions f: X→Y and g: Y→ X then X and Y have the same cardinality.


# References