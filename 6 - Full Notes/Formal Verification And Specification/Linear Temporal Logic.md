2026-05-05 20:42

Status:

Tags: 


# Linear Temporal Logic

#### Example: Temporal Properties for Mutual Exclusion 
- Mutual exclusion: at most one process in critical section at any time (i.e. in every reachable state)
- Starvation freedom  (enhanced version): whenever a process tries to enter its critical section, it will eventually succeed (along every computation path)
- No strict sequencing: processes need not enter their critical section in strict sequence (i.e. there exists a computation path along which they don't)
- We will use Linear Temporal Logic to formalise temporal properties that must hold on all paths starting in an initial state

#### Propositional Logic
- Assume a set Prop of atomic propositions
- syntax: 
	- $ϕ, ψ ::= p | tt | ¬ϕ | ϕ ∧ ψ$    $(p ∈$ Prop$)$
- Note: all other boolean operators are definable, e.g.
	- $ff ::= \neg tt$ 
	- $ϕ ∨ ψ ::= ¬(¬ϕ ∧ ¬ψ)$
	- $ϕ → ψ ::= ¬(ϕ ∧ ¬ψ)$
- models are valuations, indicating which propositions are true and which are not
	- $V : Prop → \{True, False\}$
- Semantics:
	- $V$ defines the meaning of atomic propositions 
	- truth tables define the meaning of boolean operators

#### Linear Temporal Logic (LTL)
- Transition system:
	![[Pasted image 20260505205024.png]]
- Additional assumption: each state has at least one successor 
- Some computation paths:
	- $s0 → s1 → s0 → s1 → . . .$
	- $s0 → s1 → s2 → s2 → . . .$
	- $s0 → s2 → s2 → . . .$
- LTL formulas must hold on all computation paths

#### Syntax of LTL
- Fix set Prop of atomic propositions. LTL formulas are of two kinds:
	- path formulas:
		- $tt, p$ where $p$ is an atomic proposition
		- if $f$ and $g$ are path formulas, then so are:
			- $\neg f$      not $f$
			- $f ∧ g$   $f$ and $g$ 
			- $\textbf{X} f$       at the ne$\textbf{X}$t point in time, $f$
			- $\textbf{F} f$      at some point in the $\textbf{F}$uture, $f$
			- $\textbf{G} f$     $\textbf{G}$lobally (at all future points) $f$ 
			- $f \, \textbf{U} \, g$   $f$ $\textbf{U}$ntil $g$
	- state formulas:
		- $\textbf{A} f$  along $\textbf{A}$ll computational paths, $f$ holds
	- operator precedence: unary operators $; \, \textbf{U} \, ;\,  ∧ \, and\,  ∨\,  ;\,  →$ 

#### Semantics of LTL
- Fix a transition system $M = (S, R, V)$ 
- The semantics of LTL defines:
	- when a computational path $\pi$ through $M$ satisfies a path formula $f$ 
		- Notation: $π |= f$
	- when a state $s$ of $M$ satisfies a state formula $A f$ 
		- Notation: $s |= A f$ 

#### Meaning of Temporal Operators (Pictorially)
- Let $s_0 \rightarrow s_1 \rightarrow s_2 \rightarrow . . .$ be a computation path.
	![[Pasted image 20260506111341.png]]
- Note:
	- $f$ here is a path  formula, so it is itself interpreted over paths!

#### Semantics of LTL 
- Given $π = s_0 → s_1 → s_2 → . . .$, let $π i = s_i → s_i+1 → . . .$
- Define when path formula $f$ holds on path $\pi$:
	![[Pasted image 20260506111612.png]]
- Define when state formula $A f$ holds in state $s \in S$:
	![[Pasted image 20260506111651.png]]

#### Semantics of LTL - example
![[Pasted image 20260506111929.png]]

![[Pasted image 20260506113319.png]]
![[Pasted image 20260506114755.png]]


#### LTL Patterns 
- Invariance (always): $A G p$  
	- "p remains invariantly true throughout every path"
- Guarantee (eventually): $AFp$ 
	- "p will eventually become true in every path"
- Stability (non-progress): $AFGp$ 
	- "there is a point in every path where p will become invariantly true"
- Recurrence (progress): $AGFp$ 
	- "if p happens to be false at any given point in a path, it is always guaranteed to become true again later" 
	- Same as: "p holds infinitely often"

- Response: $A G (p \rightarrow F q)$ 
	- "any state satisfying p is eventually followed by a state satisfying q"
- Precedence: $AG (p \rightarrow q U r)$ 
	- "from any state satisfying p, the system will continuously satisfy property q until property r becomes true"
- Correlation: $A(F p \rightarrow F q)$ 
	- "if p holds at some point in the future, so does q"

#### Mutual Exclusion 
- Atomic propositions:
	- $c_0, c_1$ (critical state)
	- $n_0, n_1$ (non-critical state)
	- $t_0, t_1$  (trying to enter critical state)
- Mutual exclusion: at most one process in a critical section at any time
	- $A G \neg(c_0 ∧ c_1)$ 
- Absence of starvation: whenever a process tries to enter its critical section, it will eventually succeed
	- $A G ((t_0 \rightarrow F c_0) ∧ (t_0 \rightarrow Fc_1))$
- No strict sequencing: processes need to enter their critical section in strict sequence
	- can only express negation of this property
	- this is sufficient, since counter-example to strict sequencing is proof for non-strict sequencing

#### Checking Correctness
- $A G \neg(c_0 ∧ c_1)$ 
	- Need to check that 	$\neg(c_0 ∧ c_1)$ is true at all states reachable from the initial states.
-  $A G ((t_0 \rightarrow F c_0) ∧ (t_0 \rightarrow Fc_1))$
	- Need fairness assumptions for the property to hold
		- e.g. "no process can stay in a state forever if there is an exit transition"
	![[Pasted image 20260506122338.png]]

#### LTL Formulas in SPIN
- ![[Pasted image 20260506122618.png]]
- Note $X$ can also be used, but should be used with caution
- ![[Pasted image 20260506122704.png]]

#### LTL Verification 
- Can use Promela variables or # defined symbols as atomic propositions, e.g.
	![[Pasted image 20260506122823.png]]
- In verification mode, SPIN can check for LTL property, e.g. 
	![[Pasted image 20260506122854.png]]

#### Example, Peterson's Algorithm
- ![[Pasted image 20260506123330.png]]

#### LTL Verification of Peterson's  Algorithm
- No strict sequencing:
	- assume that $[]$!($c_0$ && $c_1$)  is true
	- then the following formula captures half of the strict sequencing property:
		![[Pasted image 20260506123622.png]]
- verification of this formula fails, counterexample constitutes proof of no strict sequencing

#### Verifying the ABP using LTL
- ABP correctness:
	- "every message sent is eventually acknowledged"
- How can we verify this using LTL?
	![[Pasted image 20260506130856.png]]


#### Strong Fairness Assumptions using LTL
- SPIN only supports weak fairness assumptions 
	- but strong fairness can be enforced using LTL formulas
- Strong fairness assumption:
	![[Pasted image 20260506131623.png]]
	- where:
		- enabled(1) / enabled(2) true when the process with pid 1 / 2 (Sender / Receiver) is enabled
	- ABP correctness assuming strong fairness:
		- SF -> $[](sent \rightarrow <>ack)$
	- This restricts the runs on which the original property is checked
	![[Pasted image 20260506131843.png]]

# References