2026-04-15 13:51

Status:

Tags: 


# The Curry-Howard Correspondence

#### Lambda Calculus 
 - The essence of programming language research:
	 - small, Turing complete, foundational aspects of most PL.
 - Semantically, lambda calculus is difficult to understand, e.g. recursion through self application - what does it mean?
 - Simply typed lambda calculus eradicate these issues 

#### STLC
![[Pasted image 20260415135434.png]]


#### Properties of STLC
- STLC is deterministic:
	- no matter what reduction strategy we use, the given expression $e$ will eventually reduce to the same final value.
- STLC is terminating: 
	- no matter what reduction strategy we use, there is no expression $e$, that will reduce infinitely.
- Hence STLC is not Turing complete

#### Recursion 
- Lack of recursion/looping is a restriction in a programming language
- We can reintroduce recursion to STLC in a controlled way using types.

- We introduce fix operator that behaves as:
	![[Pasted image 20260415135932.png]]
- Example:
	- Suppose we have $N$ and $B$, if_then_else, isZero, and _ -_ . Define f as :
		![[Pasted image 20260415140025.png]]
	- Now fix f gives recursive definition of the predicate isEven

#### Natural Deduction Rules
- Rules:
	![[Pasted image 20260415140153.png]]

#### Proofs and Programs 
- There is a close correlation between proofs of natural deduction and programs in STLC.

- Functions $\tau \rightarrow \sigma$ correspond to implications $A \Rightarrow B$.
- Variables of base types correspond to propositions $p$.
	![[Pasted image 20260415140338.png]]

#### Statement 
- Theorem - Let each formula $A$ correspond to a type $\tau$ as described above, then $A_1, ... A_n ⊢ A$ is derivable in minimal intuitionistic logic (natural deduction) iff $x_1 : \tau_1, ..., x_n \tau_n ⊢ t :\tau$. 
- That is: every proof of intuitionistic natural deduction maps to a term of the simply typed lambda calculus and vise-versa. So programs can be viewed as proofs and proofs can be viewed as programs types.

#### Example Proof/Program
- Let us consider function composition as an example:
	- $λ(f : σ → δ).λ(g : τ → σ).λ(x : τ).f (g x)$ 
- And the tautology 
	- $(B ⇒ C) ⇒ (A ⇒ B) ⇒ A ⇒ C$

#### Other Logical Connectives 
- The above Curry-Howard correspondence only dealt with minimal intuitionistic logic (i.e. implication and propositions). What about the other logical connectives - conjunction, disjunction , falsity, truth?

#### Conjunction 
- ![[Pasted image 20260415141418.png]]

#### Disjunction
- ![[Pasted image 20260415141438.png]]

#### Truth and Falsity 
- ![[Pasted image 20260415141500.png]]
- The Curry-Howard Correspondence extends to full intuitionistic logic (natural deduction) and STLC with $\times, +$ Unit and Void

#### Beyond Intuitionistic Logic
- Intuitionistic logic rejects the axiom $(¬¬A ⇒ A)$.
- What program does it correspond to? Recall the type of continuations $(A \rightarrow r) \rightarrow r$ 
- Pierce law is rejected in IL $((A ⇒ B) ⇒ A) ⇒ A$. call/cc has a type $((a → b) → a) → b$.
# References