06-10-2025 16:08

Status:

Tags: [[Nondeterminism and the Subset Construction]] [[Theory of Computing]]


# Nondeterminism and the Subset Construction

#### Motivation
- This DFA:
- ![[Pasted image 20251006160857.png]]
- Over the alphabet $\{a,b\}$ accepts the language $L = \{w | w$ ends with a $b\}$ 
- It would be nice if the automaton could guess when we are about to read the last symbol and then not allow any subsequent transitions
- NFAs can do this

#### Determinism vs Nondeterminism
- Determinism:
	- Next state uniquely determined by current state and input 
- Nondeterminism:
	- Given a current state and input, there can be any number of next states (including 0)

#### Nondeterministic Transitions
- ![[Pasted image 20251006161319.png]]
- We have states and transitions as before, but:
	- There are two $b$-labelled transitions from state $0$;
	- There are no transitions from state $1$.

#### Recall: DFAs, formally 
- a DFA $M = (Q, \sum, \delta, s, F)$ 
	- $Q$ is a finite set of states;
	- $\sum$ is an alphabet;
	- $\delta : Q \times \sum \rightarrow Q$ is the transition function;
		- we will write $q \xrightarrow{a} q'$ for $\delta (q, a) = q'$;
	- $s \in Q$ is the start state;
	- $F ⊆ Q$ is the set of final states;

#### Nondeterministic finite automata (NFA)
- All remains the same except $\delta$ is now $\Delta$
- $\Delta : Q \times \sum \rightarrow 2^Q$ is the transition function
- $2^Q$ is the powerset of $Q$

#### Picture and formal presentation
![[Pasted image 20251006161656.png]]


#### Nondeterministic Acceptance
- An automaton accepts some strings (and rejects those that it doesn't accept)
- Diagrammatically: place a pebble on the initial state, move it by choosing a transition according to the symbols in the string. Accept if there is a way of choosing transitions in such a way that, when we reach the end of the string, we are in a final state, otherwise reject.
	- $abbab, babbbab$ accepted
	- $\in, abba$ rejected
- For $\sigma_{1}, \sigma_2 \in \sum$, write $q \xrightarrow{\sigma _{1}\sigma_2}q'$ when there is a $q''$ such that $q \xrightarrow{\sigma _1}q''$ and $q'' \xrightarrow{\sigma _2}q'$, and similarly for longer length strings. Write $q \xrightarrow{\in}q'$ when $q=q'$. 
- A string $x \in \sum ^*$ determines a (possible empty) set of states $q$ such that $s \xrightarrow{x}q$. $M$ accepts $x$ when there exists $f \in F$ such that $s \xrightarrow{x}f$.

#### DFAs and NFAs
- Any DFA is a special kind of NFA:
	- Compose $\delta : Q \times \sum \rightarrow Q$ with the singleton function $η : Q → 2^Q$ defined by $η(q) = {q}$ to obtain a function $δ; η : Q × Σ → 2^Q$ 
	- The acceptance conditions coincide
	- So NFAs are at least as powerful as DFAs (accept at least the languages accepted by DFAs)

#### The Power of Nondeterminism
- Q. Are NFAs more "powerful" than DFAs?
	- i.e. is there a language accepted by an NFA that cannot be accepted by a DFA?
- A. No. Any NFA can be converted to a DFA that accepts the same language. The conversion method is known as the subset construction.
- Intuition behind this construction: the resulting DFA collects all the states that could be reached by reading a given string in the original NFA in a single state

#### Subset Construction
- Let $M = (Q, Σ, ∆, s, F)$ be an NFA
- We will construct a DFA $M'$ over $\sum$  with:
	- Set of states $Q' = 2^Q$ 
	- Starting state $s' = \{s\}$
	- Final states $F'= \{X | ∃f ∈ F. f ∈ X\}$ 
	- Transition function $δ' (X, σ) = \cup _{q∈X} ∆(q, σ)$ 
- ![[Pasted image 20251006180628.png]]
- The states that correspond to subsets $\emptyset$ and {1} are unreachable: 
	- There is no path from the start state that ends in such a state.
	- Unreachable states play no part in deciding acceptance
	- Some people call state $\emptyset$ the error state.










# References