13-10-2025 17:37

Status:

Tags: [[Theory of Computing]]


# Kleene's Theorem

#### Theorem.
- If $α$ is a regexp then $L(α)$ is a regular language 
- If $L$ is a regular language then $L = L(α)$ for some regexp $α$
- In other words, finite automata and regular expressions describe the same languages.

#### NFA to regexp: Idea
- Let $M = (Q, Σ, ∆, s, F)$ be an NFA
- We want a regular expression $\alpha$ such that:
	- $L(α) = \{x | ∃f ∈ F. s \xrightarrow{x} f\}$
- That is, $\alpha$ must describe all strings $x$ which label "paths" in $M$ from some $s$ to some $f \in F$.
	- ![[Pasted image 20251013174303.png]]
	- example path: 0 a −→ 0 b −→ 1 b −→ 1 a −→ 0 b −→ 1
	- but there are infinitely many paths from 0 to 1 in the above automaton.
- Paths from 0 to 1 can be classified into:
	- Paths that only visit state 1 at the end:
		- $a^*b$
	- Paths that only visit state 1 one other time before the end: 
		- $a^*b(b+aa^*b)$
	- Paths which visit state 1 twice before the end: $a^*b(b+aa^*b)(b+aa^*b)$
	- $...$
- This is still not good enough, as we have infinitely many possibilities.

- Paths from 0 to 1 can be classified into:
	- Paths which only visit one state at the end $a^*b$ 
	- Paths that visit state 1 at least one other time $...$ 
- Idea:
	- Identify all visits to state 1 along a path from 0 to 1 $...$ 
	- $...$ so that, in between those visits, only state 0 is visited
- Solution:
	- $a^*b(b+aa^*b)^*$

#### Definition
- We will first define a regular expression $\alpha^{X}_{u, v}$ for any $X \subseteq Q$ and $u, b \in Q$.
- $\alpha^{X}_{u, v}$ describes all possible paths that start in $u$ and end in $v$ and can visit only states in $X$ as intermediate states.
- We are ultimately interested in $\alpha^{Q}_{u, v}$ for $f \in F$ (finitely many such regular expressions, so we can $+$ these)
- We will define $\alpha^{X}_{u, v}$ by recursion on $X$:
	- base case: $X = \emptyset$ 
	- inductive step: $X \cup \{q\}$ 
- For $X \subseteq Q$, we define $q \xrightarrow{x} X \, q'$ 
	- $(q \xrightarrow{\epsilon} X \, q') = (q = q')$
	- $(q \xrightarrow{\sigma} X \, q') = (q \xrightarrow{\sigma} q')$
	- $(q \xrightarrow{x\sigma} X \, q') = (∃q'' ∈ X. q \xrightarrow{x} X q'', q'' \xrightarrow{\sigma} X q* (x \neq \epsilon))$ 
- Clearly $q \xrightarrow{x} q'$ is the same as $q \xrightarrow{x} Q \, q'$;
- Idea: We want $L(\alpha^{X}_{u, v}) = \{x | u \xrightarrow{x} X \, v \}$

#### Definition of $\alpha^{\emptyset}_{u, v}$ 
- We begin with the base case of $X = \emptyset$.
- Let $a_1, ..., a_k$ be all the symbols such that $u \xrightarrow{a_i} v$ for $1 \leq i \leq k$ 
	- ![[Pasted image 20251013180305.png]]

#### Inductive step 
- Idea: a path from $u$ to $v$ in $X+\{q\}$ goes through $q$ $k$-times for some $k$ 
- ![[Pasted image 20251013180456.png]]
- $\alpha^{X}_{u, v}$ - paths that don't go through $q$;
- $\alpha^{X}_{u, q}\alpha^{X}_{q, v}$  - paths that go through $q$ once;
- $\alpha^{X}_{u, q}\alpha^{X}_{q, q}\alpha^{X}_{q, v}$ - paths that go through $q$ twice
- $...$ 
#### Definition of $\alpha^{X+\{q\}}_{u, v}$
-  $\alpha^{X+\{q\}}_{u, v} =  \alpha^{X}_{u, v} +  \alpha^{X}_{u, q}(\alpha^{X}_{q, q})^*\alpha^{X}_{q, v}$


#### NFA to regular expression
- Let $M = (Q, Σ, ∆, s, F)$ be an NFA. We know that:
	- $L(α) = \{x | ∃f ∈ F. s \xrightarrow{x}Q \, f\}$ 
- Let $f_1, ..., f_k$ be all of the states in $F$. Then:
	- $L(M) = {x | s \xrightarrow{x} Q \, f_1} ∪ ... ∪ {x | s \xrightarrow{x} Q\,  f_k}$
- The regular expression for $L(M)$ is:
	- $\alpha^{Q}_{s, f_1} + ... + \alpha^{Q}_{s, f_k}$

#### Example
# References