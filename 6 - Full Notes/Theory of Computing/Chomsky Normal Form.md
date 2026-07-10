26-10-2025 21:18

Status:

Tags: [[Theory of Computing]]


# Chomsky Normal Form

#### Normal Forms
- A CFG is in Chomsky Normal Form (CNF) when all rules are of the form
	- $A \rightarrow BC$ or $A \rightarrow a$ $(A, B, C \in N, a \in \Sigma)$ 
- A CFG is in Greibach Normal Form (GNF) when all rules are of the form
	- $A \rightarrow aB_1B_2 ...B_k$  $(k \geq 0, A, B_1, ...$ $B_k \in N, a \in \Sigma)$
- Note: No grammar in CNF or GNF can generate the empty string $\epsilon$ 

#### Examples
- Consider the CFL $L= \{a^nb^n | n \geq 1\}$ 
	- This is grammar in CNF for $L$:
		- $S \rightarrow AT | AB, T \rightarrow SB, A \rightarrow a, B \rightarrow b$
	- This is grammar in GNF for $L$:
		- $S \rightarrow aSB | aB,$ $B \rightarrow b$
- Derivations for $aabb$ are very different depending on the grammar 
- For the first grammar:
	- ![[Pasted image 20251026212415.png]]
- For the second grammar:
	- ![[Pasted image 20251026212432.png]]

#### Normal Form Theorem
- We will prove the following theorem:
	- For any CFG $G$ there exists a CFG $G'$ in Chomsky Normal Form such that:
		- $L(G') = L(G) - \{ \epsilon\}$
- A rule $A \rightarrow \epsilon$ is called an $\epsilon$-rule;
- A rule $A \rightarrow B$ is called a unit-rule;

- Let $\hat{P}$ be the smallest set containing $P$ such that:
	- if $A \rightarrow \alpha B \beta$ & $B \rightarrow \epsilon \in \hat{P}$ then $A \rightarrow \alpha \beta \in \hat{P}$;
	- if $A \rightarrow B$ and $B \rightarrow \gamma \in \hat{P}$ then $A \rightarrow \gamma \in \hat{P}$ 
- We can generate the above set by:
	- Adding the rule $A \rightarrow \alpha \beta$, whenever we find $A \rightarrow \alpha B \beta$ and $B \rightarrow \epsilon$
	- Adding the rule $A \rightarrow \gamma$, whenever we find $A \rightarrow B$ and $B \rightarrow \gamma$
- Notice that $\hat{P}$ is finite: right-hand side of new rule is substring of right-hand side of some previous rule
- Take $\hat{G} = (N, \Sigma, \hat{P}, S)$
	- Since $P \subseteq \hat{P}$, we have $L(G) \subseteq L(\hat{G})$
	- But extra rules in $\hat{p}$ are obtained by two applications of rules in $P$, so $L(\hat{G}) = L(G)$
- We now want to show that we can eliminate $\epsilon$- and unit-rules from $\hat{P}$

- CLAIM: Let $x \neq ϵ ∈ Σ ^∗$ and let $S \xRightarrow{k} x$ be a minimum-length derivation of $x$. Then no $\epsilon$-rule has been used.
- PROOF: Suppose that an $\epsilon$-rule $B \rightarrow \epsilon$ has been used:
	- ![[Pasted image 20251028205746.png]]
- The last derivation is shorter by one step which is a contradiction

- CLAIM: Let $x \neq ϵ ∈ Σ ^∗$ and let $S \xRightarrow{k} x$ be a minimum-length derivation of $x$. Then no unit-rule has been used.
- PROOF: Suppose that a unit rule $A \rightarrow B$ has been used:
	- ![[Pasted image 20251028205907.png]]
- The last derivation is one step shorter which is a contradiction

- So we do not need unit- and $\epsilon$-rules to generate non-null strings
- Obtain $G'$ by removing the $\epsilon$-rule and unit-rules from $\hat{P}$: clearly:
	- $L(G) - \{\epsilon\} = L(\hat{G} - \{\epsilon\} = L(G'))$

#### Normal Form Theorem
- For any CFG $G = (N, Σ, P, S)$ there exists CFG $G′$ with no $ϵ$- or unit rules such that $L(G ′ ) = L(G) − \{ϵ\}$.

#### Converting to CNF
- To transform any CFG $G = (N, Σ, P, S)$ into a CFG in CNF:
	- 1. Eliminate $\epsilon$- and unit-rules by following the previously described process;
	- 2. Add a new variable $X_a$ to $N$ for each constant $a \in Sigma$;
	- 3. Replace with $X_a$ any constant $a$ in all rules in $P$ (except those having one symbol on the right hand side);
	- 4. Add rules $X_a \rightarrow a$ to $P$;
	- 5. For each rule of the form $A \rightarrow B_1B_2...B_k$ with $k>2$ 
		- 5.1 Remove the rule from $P$;
		- 5.2 Add a new variable $C$ to $N$;
		- 5.3 Add rules:
			- $A \rightarrow B_1C$,              $C \rightarrow B_2...B_k$ 
	- 6. Repeat step 5 until there are no rules with more than two variables on the right hand side.
- The idea is transform rules with multiple variables on right-hand side into rules with only two variables, i.e.
	- ![[Pasted image 20251028210722.png]]

#### Example
-  $\{a ^n b^ n | n ≥ 0\} − \{ϵ\} = \{a ^n b^ n | n ≥ 1\}$.
- We start with the grammar:
	- $S \rightarrow aSb | \epsilon$ 
- Remove the $\epsilon$-rule: 
	- $S \rightarrow aSb|ab$
- We obtain the grammar for:
	- $\{a ^n b^ n | n ≥ 1\}$
- Replace constants with $X_a, X_b$ and add rules $X_a \rightarrow a, X_b \rightarrow b$:
	- $S \rightarrow X_aSX_b | X_aX_b$      $X_a \rightarrow a$     $X_b \rightarrow b$
- Introduce new variable $C$and replace $S \rightarrow X_aSX_b$ with $S \rightarrow X_aC$ and $C \rightarrow SX_b$
	- $S \rightarrow X_aC | X_aX_b$      $C \rightarrow SX_B$    $X_a \rightarrow a$    $X_b \rightarrow b$



# References