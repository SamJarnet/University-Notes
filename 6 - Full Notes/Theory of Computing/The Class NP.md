2025-12-01 14:01

Status:

Tags: [[Turing Machines]] [[Theory of Computing]]


# The Class NP

#### HAMPATH Problem
- HAMPATH = { $⟨G, s, t⟩ | G$ is a directed graph with a Hamiltonian path from s to t}
- brute-force algorithm for PATH can be adapted to HAMPATH
- we don’t know if a polynomial time algorithm for HAMPATH exists
- but if we are given a candidate Hamiltonian path, we can verify if it is a valid one in polynomial time

#### Polynomial Time Verifiers
- Recall: A decider for a language $L$ accepts an input $w$ iff $w \in L$.
- A verifier for $L$ takes an additional input $c$, and checks whether $c$ is a witness for $w \in L$.
	- e.g. a verifier $V$ for HAMPATH additionally takes a candidate Hamiltonian path as input, and checks whether it is a Hamiltonian path
	- the verifier $V$ is "correct" if the following holds:
		- A graph $G$ has a Hamiltonian path iff $V$ accepts $⟨G, c⟩$ for some $c$.

#### Definition
- Definition. A verifier for language L is an algorithm V such that $L = \{w | V$ accepts $⟨w, c⟩$ for some string $c\}$
- If V accepts ⟨w, c⟩ then c is called certificate (proof) of w ∈ L.
- A polynomial time verifier is one which runs in polynomial time in the length of w.
- Key observation:
	- A polynomial time verifier can only explore a part of $c$ of size polynomial in the length of $w$.

#### Example: Verifier for HAMPATH
- We give a verifier $V$ for HAMPATH which
	- Takes an input $⟨G, s, t, c⟩$ with $c$ a candidate Hamiltonian path in $⟨G, s, t⟩$
	- Accepts $⟨G, s, t, c⟩$ iff $c$ is an actual Hamiltonian path from $s$ to $t$ in $G$
- On input $⟨G, s, t, c⟩$:
	- 1. Check if $c$ encodes a list $v_1, ..., v_n$ with $n$ the number of nodes in $G$. If not, reject.
	- 2. Check for repetitions in the list $v_1, ..., v_n$. if any found, reject.
	- 3.  Check whether $v_1 = s$ and $v_n = t$. If either fails, reject.
	- 4. For each $i \in \{1, ..., n-1\}$:
		- 5. Check whether $(v_i, v_{i+1})$ is in an edge of $G$. If it is not, reject.
	- 6. Accept.
- This is a verifier for HAMPATH:
	- $⟨G, s, t⟩ ∈ HAMPATH$ iff $V$ accepts $⟨G, s, t, c⟩$ for some $c$.

#### Polynomial Time Verifier for HAMPATH
- To be a polynomial time verifier, $V$ must run in polynomial time in the size of $⟨G, s, t⟩$.
- $V$ runs in polynomial time in the number of nodes $n$ of $G$:
	- Each stage runs in polynomial time
	- Stage 5 is repeated $n$ times
- Since the length of $⟨G, s, t⟩$ is polynomial in $n$, $V$ also runs in polynomial time in the length of $⟨G, s, t⟩$. 

#### The class of NP
- Definition:
	- NP is the class of languages which have polynomial time verifiers.
- So $HAMPATH \in NP$ 
- $NP=$ Non-Deterministic Polynomial.

#### A Non-Deterministic Algorithm for HAMPATH
- On input $⟨G, s, t⟩$:
	- 1. Non-Deterministically choose nodes $v_1, ..., v_n$ where $n$ is the number of nodes in $G$.
	- 2. Check for repetitions in the list $v_1, ..., v_n$. if any found, reject.
	- 3.  Check whether $v_1 = s$ and $v_n = t$. If either fails, reject.
	- 4. For each $i \in \{1, ..., n-1\}$:
		- 5. Check whether $(v_i, v_{i+1})$ is in an edge of $G$. If it is not, reject.
	- 6. Accept.
- Note:
	- The computation of this non-det. algorithm is a tree. This can be split into a guessing phase (stage 1, non-det) and a checking phase (stages 2-6, det)
- Above algorithm runs in non-det. polynomial time in the number of nodes in $G$:
	- Stage 1 takes polynomial time 
	- Stage 2-6 are as before, so take polynomial time.

#### An alternative Definition of the class NP
- Definition (alternative).
	- NP is the class of languages that can be decided by a non-deterministic Turing machine in polynomial time.
- Theorem. 
	- $L \in NP$ iff $L$ can be decided by some non-deterministic polynomial time TM.

#### The Complexity Class NTIME$(t(n))$
- Definition:
	- Let $t: \mathbb{N} \rightarrow  \mathbb{R}^+$ be a function. The time complexity class  NTIME$(t(n))$ consists of all languages that can be decided by an $O(t(n))$ time non-deterministic TM.
- Corollary: 
	- $NP = \bigcup_{k∈N} NTIME(n^k)$ 
- The class of NP is robust:
	- It does not depend on the choice of non-det computation model.

#### Example of NP problems
- Anything P is also in NP. If a language can be decided in polynomial time by a deterministic TM, then also by a non-det TM.
	![[Pasted image 20251201143112.png]]
	
#### NP Problems: SAT
- SAT: Boolean satisfiability 
- Given a boolean expression, e.g.:
	- $(x ∨ y ∨ ¬z) ∧ (w ∨ ¬z) ∧ (¬w ∨ x)$ 
- Does there exist an assignments of $0$s and $1$s to the variables $(w, x, y, z)$ such that the formula is satisfied?
	- $SAT = \{⟨ϕ⟩ | ϕ$ is a satisfiable Boolean formula }
- Instances of SAT:
	- $(x ∨ y) ∧ (¬x ∨ ¬y) ∧ (x ∨ z)$
		- yes : e.g. x = 1, y = 0, z = 0 is a satisfying assignment
	- $x ∧ y ∧ (¬x ∨ z) ∧ (¬y ∨ ¬z)$
		- no : always FALSE

- SAT is in NP: we can non-deterministically generate all possible assignments of 0/1 to the variables, then substitute each of them in the formula to see if it is satisfied:
	- On input $⟨ϕ⟩$, with $ϕ$ a boolean expression over $x_1, ... x_n$:
		- 1. Non-deterministically choose values $v_i \in \{0, 1\}$ for $x_i, i \in \{1, ..., n \}$ 
		- 2. Evaluate $\phi$ using these values.
		- 3. If the result is true, accept; otherwise reject.
	- This takes non-det poly time in the size of $⟨ϕ⟩$ (= number of symbols needed to encode $\phi$):
		- Each stage can be implemented in poly time
- We don't know if $SAT \in P$ 

#### NP Problems: TSP(D)
- TSP(D) Travelling Salesperson Problem (Decision version)
- Given a number $D$ and $n$ cities $c_1, ..., c_n$ with given distances between them:
	- $d(c_i, c_j) = d_{i,j}$ 
- Is there a circular route that visits each city exactly once, with total distance at most $D$?
	![[Pasted image 20251201144603.png]]
- TSP(D) is in NP: the non-det machine can just "guess" an order in which to visit the cities, and then check that it is a valid route with total distance at most $D$. This can be done in non-det poly time. 

#### NP Problems: 3COL
- 3COL: 3-colourability
- Given a graph $G$, is it possible to colour the vertices with at most 3 colours, such that no two adjacent vertices have the same colour?
	![[Pasted image 20251201144837.png]]
- 3COL is in NP: We can "guess" the colour of each vertex and check that the resulting colouring is valid. This can be done in non-det poly time
- We don't know if 3COL is in $P$.

#### P = NP?
- There are lots of NP problems like SAT, TSP(D) and 3COL for which the best known algorithm runs in exponential time. 
- But no one has been able top prove that the only algorithms for these problems are exponential
- In fact we don't know whether P = NP. Do there exist problems in NP which are not in P?
	- We suspect yes, but no one has proved it yet.
# References