02-11-2024 15:38

Status:

Tags: [[Mathematics I]] [[Sets]] [[Relations Between Sets]] 


# Equivalence Relations

#### Definition:
- An equivalence relation ~ on $X \,(\:\sim\: \subseteq X \times X)$ is a special relation that satisfies the following three axioms:
	- reflexivity: $\forall \: x \in X$. $x \sim x$ (relates to itself)
	- symmetry: $\forall \: x,y \in X$. if $x \sim y$ then $y \sim x$ 
	- transitivity: $\forall \: x,y,z \in X$.  if $x \sim y$ and $y \sim z$ then $x \sim z$ 

#### Examples and non examples:
- Let P = set of people in this room
	- Let R = { (x,y) | x ∈ P and y ∈ P have the same first name } - Yes
- Let C = set of cities in the UK 
	- S = { (x,y) | x ∈ C and y ∈ C are less than 50 miles from each other } - No as Southampton could be 50 from London but London could be 50 from somewhere else 

#### Equivalence class
- If ~ is an equivalence relation on X and $a \in X$ then the equivalence class of $a$ is the set:
	- $[a] = \{x\: |\: x \in X \, and \,x  \sim a\}$   
- notice that the reflexivity of ~ implies that $a \in [a]$
- $X/\sim = \{[x]\:|\:x \in X\}$ is the set of equivalence relations 

#### Partitions
- A collection $X_1, …, X_n$ of subsets of X is a partition of a set X when:
	- $X_1 \cup … \cup X_n = X$ 
	- for all 1≤ i, j ≤ n, i ≠ j implies that $X_i \cap X_j = \emptyset$ 
	- For any equivalence relation on a set, you can create a partition where each subset is an equivalence class. Conversely, given any partition of a set, you can define an equivalence relation where two elements are equivalent if they belong to the same subset in the partition


#### Quotients:
- If ~ is an equivalence relation on X then the set X/~ of equivalence classes is sometimes called the quotient of X with respect to ~

#### Orders:
- We know that 0 <= 1, 4 <= 56 and $3 \leq \pi \leq 4$ 
- The order symbol is actually a relation:
	- $\leq N = \{(p, q)\: | \:p,q \in N, \exists \: r \in N. q=p+r\}$ 
	- $\leq N = \{(x, y)\: | \:x,y \in N, \exists \: r \in R. y=x+r\}$

#### Partial orders:
- A relation $\leq \, \subseteq X \times X$ is a partial order when it is:
	- reflexive: $\forall \, x \in X$. $x \leq x$ and $y \leq z$  imply $x \leq z$  
	- transitive: $\forall \, x,y,z \in X. x \leq y \, and \, y \leq x \, then \, x=y$ 
	- anti-symmetric: if $\forall \, x,y.$ if $x \leq y$ and $y \leq x$ then $x=y$  
# References