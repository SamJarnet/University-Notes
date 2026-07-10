2025-12-03 22:12

Status:

Tags: [[Theory of Computing]] [[Turing Machines]]


# Space Complexity

#### Complexity
- Recall:
	- The time complexity of a decider $M$ is the function $f:\mathbb{N} \rightarrow \mathbb{N}$ where $f(n)$ is the maximum number of steps $M$ uses on any branch of its computation, on any input of length $n$ 
- Space complexity definition:
	- The space complexity of a decider $M$ is the function $f:\mathbb{N} \rightarrow \mathbb{N}$ where $f(n)$ is the maximum number of tape cells $M$ scans on any branch of its computation, on any input of length $n$. 
	- We say that $M$ is an $f(n)$ space Turing Machine

#### The Complexity Classes $SPACE(f(n))$ and $NSPACE(f(n))$
- Definition. Let $f:\mathbb{N} \rightarrow \mathbb{R}^+$ be function
- The complexity class $SPACE(f(n))$ is the collection of all languages that are decidable by an $O(f(n))$ space deterministic TM.
- The complexity class $SPACE(f(n))$ is the collection of all languages that are decidable by an $O(f(n))$ space non-deterministic TM.
  

#### Example: SAT 
- Recall: we can't solve SAT with a p.t. alg.
- What about polynomial space?
	- Here is a (deterministic) polynomial space algorithm for SAT:
		- On input $⟨ϕ⟩$, with $ϕ$ a boolean expression in variables $x_1, ..., x_n$: 
			- 1. For each assignments to to the variables $x_1, ... , x_n$ 
				- 2. Evaluate $ϕ$ on that assignment 
			- 3. If $ϕ$ ever evaluates to 1 then accept; otherwise reject
	- Above runs in polynomial space, as it can reuse space:
		- Only the current assignment needs to be stored ($O(n)$ space)
		- Evaluating $ϕ$ can be done with $O(m)$ space, where $m$ is the size of $ϕ$

  
#### Relating Space and Time complexity
- If a NTM /alg. runs in $f(n)$ time, how much space does it use?
	- At most $f(n)$
- If a NTM/alg. uses $f(n)$ space, how much time does it use?
	- Theorem. Let $f:\mathbb{N} \rightarrow \mathbb{R}^+$ be function be such that $f(n) \geq n$ for all $n$. If a decider runs in $f(n)$ space, then it runs in $2^{O(f(n))}$ time.

- Proof idea:
	- There are at most $|Q| * f(n)*2^{O(f(n))}$ possible configurations:
		- $|Q|$ states
		- $f(n)$
		- $2^{O(f(n))}$ 
	- A decider will not repeat configurations (on any branch)
	- So the longest the decider can run is $|Q| * f(n)*2^{O(f(n))}$ steps
	- $|Q| * f(n)*2^{O(f(n))}$ is $2^{O(f(n))}$ 


#### PSPACE and NPSPACE
- Definition:
	- The class PSPACE is the set of all languages that can be decided by a deterministic TM using polynomial space:
		- PSPACE = $\bigcup_{k \in \mathbb{N}}$ SPACE$(n^k)$ 
  - Definition:
	- The class NPSPACE is the set of all languages that can be decided by a non-deterministic TM using polynomial space:
		- NPSPACE = $\bigcup_{k \in \mathbb{N}}$ NSPACE$(n^k)$ 
  
- Anything in PSPACE is in NPSPACE. If a language can be decided by using polynomial space by a deterministic TM, then also by a non-deterministic one:
	![[Pasted image 20251204175541.png]]

#### PSPACE = NPSPACE?
- Recall:
	- For $f(n) \geq n$, every $f(n)$ time non-deterministic TM has an equivalent $2^{O(f(n))}$ time deterministic TM
- This are different with space:
	- Savitch Theorem:
		- Let $f : \mathbb{N} \rightarrow \mathbb{R}^+$ be such that $f(n) \geq n$ for all $n$. Then every $f(n)$ space non-deterministic TM has an equivalent $f(n)^2$ space deterministic TM.
- Corollary:
	- PSPACE = NPSPACE

#### Relationships between Complexity Classes
- P $\subseteq$ PSPACE:
	- A deterministic TM which runs in polynomial time can only use polynomial space
- NP $\subseteq$ NPSPACE:
	- Similar reason
- Hence, using Savitch's theorem, NP $\subseteq$ PSPACE
- PSPACE $\subseteq$ EXPTIME:
	- For $f(n) \geq n$, if a decider runs in $f(n)$ space, then it runs in $2^{O(f(n))}$ time.
	- For $f(n) = n^k, 2^{O(f(n))}$ is $O(2^{n^{k+1}})$.
	![[Pasted image 20251204180657.png]]
- We don't know which of these inclusions are strict
- All we know is P $⊊$ EXPTIME ($⊊$ denotes strict subset)
 - Note:
	 - We can also define EXSPACE/ We know that:
		 - PSPACE $⊊$ EXPSPACE,    EXPTIME $⊊$ EXSPACE 

# References