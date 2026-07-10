2025-11-19 22:02

Status:

Tags: [[Theory of Computing]]  [[Reductions]]


# Decidable Problems

#### Theorem 1
- Prove: $A_{DFA} = \{⟨B, w⟩|$ $B$ is a DFA that accepts input string $w\}$ is recursive:
	- We define a TM $M$ that decides $A_{DFA}$.
	- $M =$ On input $⟨B, w⟩$, where $B$ is a DFA and $w$ is a string:
		- Simulate $B$ on $w$
		- If simulation ends in accept state, accept. If it ends in non-accepting state, reject.

#### Theorem 2
- Prove $E_{DFA} = \{⟨A⟩ | A$ is a DFA and $L(A)= \emptyset \}$ is recursive:
	- A DFA accepts some stings iff reaching an accept state from the start state by travelling along the arrows of the DFA is possible. 
	- To test this condition, we can design TM $T$ that uses a marking algorithm
	- $T$ On input $⟨A⟩$, where $A$ is a DFA:
		- 1. Mark the start state of $A$ 
		- 2. Repeat until no new states get marked:
			- 2.1 Mark any state that has a transition coming into it from any state that is already marked 
		- If no accept state is marked, accept; otherwise, reject.

#### Theorem 3
- Prove $EQ_{DFA} = \{⟨A, B⟩ | A, B$ are a DFAs and $L(A) = L(B)\}$ is recursive:
	- $T =$ On input $⟨A, B⟩$ where $A, B$ are DFAs:
	- Construct DFA $C$ for symmetric difference of $L(A)$ and $L(B)$, i.e.
		- $L(C) = (L(A) \cap (L(B))^c) \cup ((L(A))^c) \cap L(B))$
		![[Pasted image 20251123172701.png]]
	- Run TM $T'$ from Theorem 2 on input $C$, i.e. check if $L(C) = \emptyset$ 
	- If $T'$ accepts, accept. If $T'$ rejects, reject.

#### Theorem 4
- Prove $A_{CFG} = \{⟨G, w⟩ | G$ is a CFG that generates string $w\}$ is recursive:
	- Cannot  go through all derivations to determine whether any is a derivation of $w$: possible infinitely many.
	- If $G$ does not generate $w$, this algorithm would never halt.
	- We need to ensure that the algorithm tries only finitely many derivations.
	- In any $G$ in CNF, any derivation of $w$ has $2n-1$ steps, where $n \geq 1$ is the length of $w$.
	- Only finitely many such derivations exist.
	- $T=$ On input $⟨G, w⟩$, where $G$ is a CFG and $w$ is a string:
		- Convert $G$ into an equivalent grammar in CNF.
		- List all derivations with $2n-1$ steps, where $n$ is the length of $w$. If $n=0$ list all derivations with one step.
		- If any of these derivations generate $w$, accept, if not, reject.

####  Theorem 5
- $E_{CFG} = \{⟨G⟩ | G$ is a CFG and $L(G) = \emptyset \}$ 
	- We need to test whether the start variable can generate a string of terminals (i.e. a sentence)
	- First, the algorithm marks all the terminal symbols in the grammar. 
	- Then, it scans all the rules of the grammar.
	- If it finds a rule that permits some variable to be replaced by some string of symbols, all of which are already marked, too.
	- The algorithm continues in this way until it cannot mark any additional variables
	- $T$ = On input $⟨G⟩$, where $G$ is a CFG:
		- Mark all terminal symbols in $G$
		- Repeat until no new variables get marked:
			- Mark any variable $A$ where $G$ has rule $A \rightarrow U_1 ... U_n$ and each symbol $U_1...U_n$ has already been marked.
		- If start variable is not marked, accept, otherwise, reject. 
# References