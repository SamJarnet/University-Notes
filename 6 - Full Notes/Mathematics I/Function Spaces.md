02-11-2024 17:09

Status:

Tags: [[Mathematics I]] [[Sets]] [[Functions Between Sets]]


# Function Spaces

#### The graph of a function:
- We have been vague about what is a function, considered as a set
- in set theory, functions are identified with their graphs
- Given a function $f: X \rightarrow Y$,  its graph is the set of pairs $\{(x, f(x)) \, | \, x \in X\}$ 

![[Pasted image 20241102171738.png|500]]

#### Function Spaces:
- Given sets X and Y, let $Y^X$ denote the set of all functions from X to Y
- There is an important function $ev: \, X \times Y^X \rightarrow Y$.  This function takes the input (x, f) and applies the function f to x
- Questions:
	- Let $\mathbb{2} = \{0, 1\}$ , the elements of ${\mathbb{2}}^{\mathbb{2}}$ are {(0,0),(0,1),(1,0),(1,1)}
	- $|Y|^{|X|}=|Y|^{|X|}$ 
	- $|\emptyset^{\emptyset} |$ = 1

#### Powersets:
- Given a set X, the powerset P(X) or $2^X$ is the set of all subsets of X
- Examples:
	- P({0,1}) = { ∅, {0}, {1}, {0,1} }
	- P({a, b, c}) = { ∅, {a}, {b}, {c}, {a, b}, {a, c}, {b, c}, {a, b, c} }
	- P(∅) = {∅}
	- PP(∅) = P({∅}) = { ∅, {∅} }
- |P(X)| = $2^{|X|}$ 
# References