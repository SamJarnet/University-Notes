06-10-2025 18:09

Status:

Tags: [[Theory of Computing]]


# Epsilon NFAs

#### Epsilon Moves
- We have seen that nondeterminism can be tamed
	- The price: possible exponential increase in the number of states
- We need one more useful feature: $\epsilon$-moves
- ![[Pasted image 20251006181133.png]]
- Idea:
	- In the pebble game you can always take an $\epsilon$-labelled transition without "consuming a symbol"

#### Nondeterministic finite automata with $\epsilon$-moves
- an $\epsilon$NFA $M = (Q, Σ, θ, s, F):$ 
- $Q$ is a finite set of states;
- $\sum$ is an alphabet;
- $θ : Q × (Σ ∪ {\epsilon}) → 2^Q$ is the transition function;
	- We will write $q \xrightarrow{\sigma}q'$ for $q' \in θ(q, σ)$;
- $s$ is the start state
- $F ⊆ Q$ is the set of final states

#### Acceptance in $\epsilon$NFAs
- Write $q \xRightarrow{\epsilon}q'$ if either $q=q'$ or there exists a sequence of $\epsilon$-moves $q \xrightarrow{\epsilon} . . . \xrightarrow{\epsilon} q'$;
- Write $q \xRightarrow{\sigma}q'$ (for $\sigma \in \sum$) if there exists a sequence $q\xRightarrow{\epsilon} \xrightarrow{\sigma} \xRightarrow{\epsilon} q'$;
- Write $q \xRightarrow{\sigma \tau}q'$ if we have $q\xRightarrow{\epsilon} \xrightarrow{\sigma} \xRightarrow{\epsilon} \xrightarrow{\tau}\xRightarrow{\epsilon}  q'$, and similarly for longer strings
- A string $x$ is accepted if there exists $f \in F$ such that $s \xRightarrow{x} f$.

- ![[Pasted image 20251006182354.png]]

#### The Power of $\epsilon$-moves
- Any NFA is a special kind of $\epsilon$NFAs (one that has no $\epsilon$-transitions)
- Q. Are $\epsilon$NFAs more powerful than NFAs?
- A. Any $\epsilon$NFA can be turned into an NFA
- So $\epsilon$NFAs accept precisely the regular languages

#### From $\epsilon$NFAs to NFAs
- Let $M$ be an $\epsilon$NFA. Let $M'$ be an NFA with the same states but:
	- $∆'(q, σ)  = \{q'| q \xRightarrow{\epsilon}\xrightarrow{\sigma}  q' \}, F' = \{q | ∃f ∈ F. q " \xRightarrow{\epsilon} f\}$ 
	- $\epsilon$-transitions removed;
	- states with $\epsilon$-transitions to a final state become final;
	- new transitions added to preserve the language.
	- ![[Pasted image 20251006183843.png]]
	- Claim $L(M') = L(M)$ 
  
  
  
  
# References