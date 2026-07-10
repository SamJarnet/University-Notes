2025-12-01 15:04

Status:

Tags: [[Turing Machines]] [[Theory of Computing]] [[The Class NP]]


# NP Completeness
#### The class EXPTIME
- EXPTIME is the class of languages that can be decided by a det TM in exponential time:
	- EXPTIME = $\bigcup_{k \in \mathbb{N}} TIME(2^{n^k})$ 
- Note: in the above, $n$ is the size of the input and $k$ is the constant
	- HAMPATH, SAT, 3COL $\in$ EXPTIME (use brute-force)
	- We will prove that NP $\subseteq$ EXPTIME
	- But we don't know if NP is contained in a det time complexity class that is strictly smaller than EXPTIME.

#### Polynomial Time Reduction
- Q: If we can reduce one language (decision problem) $A$ to another language (decision problem) $B$, then does a polynomial time algorithm for $B$ give us a polynomial time algorithm for $A$?
- A: It depends on how fast the reduction can be computed. if the translation algorithm runs in exponential time, the above is clearly false. 

#### Polynomial Computable Functions
- A function $f: \Sigma ^* \rightarrow \Delta ^*$  is polynomial time computable if there exists deterministic TM that halts on each input $w \in \Sigma ^*$ with just $f(w)$ on its tape. 

#### Polynomial Time Reduction
- Let $A \subseteq \Sigma ^*$ and $B \subseteq \Delta ^*$ can be two languages. A polynomial time reduction from $A$ to $B$ is a function $f: \Sigma ^* \rightarrow \Delta ^*$, such that:
	- $f$ is computable in polynomial time;
	- for all $x \in \Sigma ^*$, we have:
		- $x  \in A$ iff $f(x) \in B$ 
- We write $A \leq_P B$ if a polynomial time reduction from $A$ to $B$ exists. 
	 ![[Pasted image 20251201151506.png]]

- If $f$ is a polynomial time reduction from $A$ to $B$, and we can find a polynomial time algorithm for $B$, then this automatically gives us a polynomial time algorithm for $A$:
	- Instance of $A \rightarrow$ Poly time reduction $f \rightarrow$ instance of $B \rightarrow$ Poly time alg. for $B \rightarrow$ "yes/no"
- Given an instance $x \in \Sigma^*$ of problem $A$, compute $f(x)$ and run the algorithm for deciding $B$ on it. This will tell us whether $x$ is a "yes" instance of $A$. The time taken to do all of this is polynomial.
- Theorem:
	- If $A \leq_P B$ and $B \in P$, then $A \in P$ 
- Corollary:
	- If $A \leq_P B$ and $A \notin P$, then $B \notin P$

#### Polynomial-Time reduction of 3COL to SAT
- As a classic example of polynomial time reduction, let's reduce 3COL TO SAT. 
- Recall that 3COL and SAT are both problems we don't have a polynomial time algorithm for.
- If we can do this reduction, then a polynomial time algorithm for SAT gives us a polynomial time algorithm for 3COL.

- Our task: Given a graph $G$, find a transformation of $G$ to a boolean expression $\phi$, such that $\phi$ is satisfiable precisely when $G$ is 3-colourable. The transformation must be computable in polynomial time.+
	![[Pasted image 20251201152556.png]]
- We want: $\phi$ is satisfiable iff $G$ is 3-colourable
- So assignments to the variables of $\phi$ must encode colourings of $G$ 
- But a single boolean variable cannot encode a choice of colour for a node
- So for each node $v_i$ of $G (i \in \{1, .. m\})$, we use three boolean variables, for a total of $3m$ variables ($m=\#$nodes):
	- $r_i : 1$ precisely when $v_i$ is RED.
	- $g_i : 1$ precisely when $v_i$ is GREEN.
	- $b_i : 1$ precisely when $v_i$ is BLUE.

- The formula $\phi$ must capture the colouring constraints on the graph. These are of 3 types:
	- 1. For each node $v_i$, the expression:
		- $(r_i ∨ g_i ∨ b_i)$ 
		- Must be true (each node has at least one colour )
	- 2. For each node $v_i$, the expression:
		- $¬(r_i ∧ g_i) ∧ ¬(r_i ∧ b_i) ∧ ¬(g_i ∧ b_i)$ 
		- Must be true (each node has  at most on colour)
	- 3. For each edge $e_{i, j}$ of $G$, we need constraints:
		-  $¬(r_i ∧ r_j) ∧ ¬(g_i ∧ g_j) ∧ ¬(b_i ∧ b_j)$ 
		- (Adjacent nodes cannot have the same colour)

- We can now combine all of these constraints into a boolean expression $f(G)$ using $∧$.
- The expression $f(G)$ is satisfiable precisely when there exists an assignment of exactly one colour to each graph node, such that adjacent nodes have different colours.
	![[Pasted image 20251201153702.png]]
- So we have the required mapping $f$ from graphs to boolean expressions
- Q: Can $f(G)$ be computed in poly time (in the size of $G$)?
- A: Let m=#nodes, I=#edges in $G$.
	- There are $O(m)$ variables
	- each variable $(r_i , g_i , b_i )$ appears in $f(G)$ $O(1)+ O(I)$  times, 
	- the number of additional symbols ("(", ")", "$∧$", $∨$", "$¬$") is $O(m+I)$.
- So the length of $f(G)$ is polynomial in the size of $G$
- Moreover, one pass through the encoding of $G$ suffices to compute $f(G)$.
- So $f$ can be computed in poly time

- We have found a polynomial time reduction of 3COL to SAT. 
- If we subsequently find a polynomial time algorithm for SAT, this gives us one for 3COL as well.
- Conversely, if we can prove that there is no polynomial time algorithm for 3COL, then there can’t be one for SAT either
	![[Pasted image 20251201161038.png]]

#### Hard Problems
- Q: What is meant by an "NP-Hard" problem
- A: It is a problem which is as hard as any problem in NP.
- If we can reduce all NP problems to some problem in poly time, then a poly time algorithm for that problem leads to poly time algorithms for all NP problems.

#### The Cook-Levin Theorem
- This theorem says that not only can 3COL be reduced to SAT in p.t. but every problem in NP can be reduced to SAT in p.t
- So SAT is at least as hard as any other NP problem
- Then if we can find a p.t. alg. for SAT, then we also have one for every NP problem, and so
	- P = NP

#### NP-hard and NP-complete Problems
- A language (decision problem) B is called NP-hard if every language (decision problem) A in NP is p.t. reducible to B.
- If be is also in NP, it is called NP-complete 
- If any NP-hard or NP-complete language is in P, then P = NP

#### NP-Hard and NP-Complete Problems
- Cook and Levin showed that SAT is NP-complete
	![[Pasted image 20251203121827.png]]
- To prove that another problem X is NP-complete, we only have to show it is in NP and then find a polynomial time reduction from SAT to X.
- Then there must be a polynomial time reduction from any NP problem to X (via SAT)
- If Y is an NP-hard problem and there exists a polynomial time reduction from Y to some problem X, then X is also NP-hard
- Using this rule, we can now find lots of NP-complete problems, including 3COL and TSP(D)
	![[Pasted image 20251203122030.png]]
- So if we find a p.t. alg. for any of these, then there must be a p.t. alg. for every NP problem, i.e. P = NP.










# References