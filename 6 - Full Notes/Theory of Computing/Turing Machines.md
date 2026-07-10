2025-11-03 15:02

Status:

Tags: [[Theory of Computing]]


# Turing Machines

#### Informal Description
- ![[Pasted image 20251103151457.png]]
- Deterministic one-tape Turing machine $M$
- A finite set of states $Q$
- Semi-infinite tape delimited on the left by endmarker $⊢$
- A head that moves left and right on the tape, reading and writing symbols
- Input string is of finite length, written on contiguous cells starting with $⊢$, followed by infinitely many cells on the right with black symbol $⊔$.

- $M$ starts in initial state $s$, head scans endmarker  $⊢$
- At each step, $M$ reads symbol on tape under head, and, depending on current symbol, writes a new symbol and moves either left or right
- Action taken at each step is determined by a transition function $\delta$ 
- Transition is deterministic
- $M$ accepts input after accept state $t$
- $M$ rejects input after entering reject state $r$
- $M$ may loop and run indefinitely without even accepting or rejecting input

#### Formal Definition
- A deterministic one-tape Turing machine is a 9-tuple: 
	- $M = (Q, Σ, Γ, ⊢, ⊔, δ,s, t,r)$
- Where:
	- $Q$ is a finite set of states;
	- $Σ$ is a finite set (input alphabet);
	- $Γ$ is a finite set (tape alphabet) such that $Σ ⊆ Γ$;
	- $⊢ ∈ Γ$ \ $Σ$ is the left endmarker;
	- $⊔ ∈ Γ$  \ $Σ$ is the blank symbol; 
	- $δ : Q × Γ → Q × Γ × \{L, R\}$ is a transition function;
	- $s ∈ Q$ is the start state; 
	- $t ∈ Q$ is the accept state;
	- $r ∈ Q$ is the reject state, with $r \neq t$.

#### Transitions 
- $δ : Q × Γ → Q × Γ × \{L, R\}$
- A transition:
	- $\delta(p, a) = (q, b ,d)$
- Means:
	- When in state $p$ scanning $a$ on tape, replace it with $b$, move head in direction $d$ (left or right) and enter state $q$
- TM never moves off tape to left of endmarker, i.e. for all $p \in Q$ there exists $q \in Q$ such that
	- $δ(p, ⊢) = (q, ⊢, R)$
- Once TM accept or reject state, it never leaves it, i.e. for all $b \in \Gamma$ there exists, $c, c' \in \Gamma$ and $d, d' \in \{L, R\}$
	- $δ(t, b) = (t, c, d)$,       $δ(r, b) = (r, c', d')$.
- State set and transition together are referred to as "state control"

#### Example
- A TM that accepts:
	- $\{a^nb^nc^n| n \geq 0\}$
- TM starts in $s$, scans right to check if input string has form $a^*b^*c^*$ 
- Machine does not change anything (i.e. replace each symbol with the same symbol)
- TM replaces first blank symbol $⊔$ with right endmarker $⊣$
- TM scans left, erases first $c$, then first $b$, then first $a$ until $⊢$ 
- TM scans right, erases one $a$, one $b$ and one $c$
- TM continues same process
- If TM sees one occurrence of a letter and no occurrence of another, it rejects
- If TM erases all letters, and only blanks between $⊢$ and $⊣$  remain, it accepts

- Formal definition:
	- $Q = \{s, q1, . . . , q10, t,r\}, Σ = \{a, b, c\}, Γ = Σ ∪ \{⊢, ⊔, ⊣\}$ 
- Transition function $\delta$:
	- ![[Pasted image 20251103215835.png]]
- Transitions for $t$ and $r$ can be defined as explained above

#### Configurations
- At any point tape of TM contains semi-infinite string:
	- $⊢y⊔⊔⊔⊔⊔⊔⊔⊔⊔ · · ·$ 
- Where:
	- $y \in \Gamma^*$
- A configuration is an element of:
	- $Q × \{⊢y⊔⊔⊔ · · · | y ∈ Γ ^∗ \} × \mathbb{N}$
- With:
	- $\mathbb{N} = \{0, 1, 2, ...\}$
- A configuration:
	- $(p, z, n)$
- Specifies current state $p$, current tape contents $z$ and current position of read/write head $n \geq 0$
- We use $\alpha \beta, \gamma,$ etc. to denote configurations
- Start configuration on input $x \in \Sigma ^*$ 
	- $(s,⊢x⊔⊔⊔ . . . , 0)$
- For:
	- $z ∈ \{⊢y⊔⊔⊔ · · · | y ∈ Γ ^∗ \},$
- Let the $z_n$ be the $n$th symbol of $z$.
- Let $s^n_b(z)$ demote the string obtained from $z$ by replacing $z_n$ with $b$ at $n$
	- $s^4 _b (⊢baaacabca · · · ) =$  $⊢baabcabca · · ·$
- Define a next configuration relation $\xrightarrow{1}$ as follows
	![[Pasted image 20251104221723.png]]
- Tape contains $z$, TM is in state $p$ scanning $n$th cell, then prints $b$, goes left (right), enters state $q$ 
- Result: tape contains $s^m_b(z)$, head at $n-1$st cell ($n+1$st cell) and TM in state $q$ 

#### Computation: Acceptance and Rejection
- Define the transitive closure $\Rightarrow$ of $\xrightarrow{1}$ inductively as follows:
	- $\alpha \xrightarrow{0} \alpha$
	- $\alpha \xrightarrow{n+1} \beta$ if $\alpha \xrightarrow{n} \gamma \xrightarrow{1} \beta$, and 
	- $\alpha \Rightarrow \beta$ if $\alpha \xrightarrow{n} \beta$ for some $n \geq 0$.
- $\alpha \Rightarrow \beta$ means that there is a computation of $\beta$ from $\alpha$.
- A TM $M$ accepts an input $x \in \Sigma ^*$ if 
	- $(s, ⊢x⊔⊔⊔ . . . , 0) ⇒ (t, y, n))$
- For some $y$ and $n$.
- A TM $M$ rejects an input $x \in \Sigma ^*$ if 
	- $(s, ⊢x⊔⊔⊔ . . . , 0) ⇒ (r, y, n))$
- For some $y$ and $n$.

#### Example (Continued)
- TM that accepts:
	- $\{a^nb^nc^n| n \geq 0\}$
- $Q = \{s, q1, . . . , q10, t,r\}, Σ = \{a, b, c\}, Γ = Σ ∪ \{⊢, ⊔, ⊣\}$ 
- Transition function
	![[Pasted image 20251106201458.png]]

- On $abc$:
	![[Pasted image 20251106201522.png]]
- The string $abc$ is accepted
- On $ab$
	![[Pasted image 20251106201539.png]]	
- The string $ab$ is rejected

#### Total Turing Machines
- A TM $M$ is said to halt on input $x$ if it either accepts or rejects $x$.
- It is possible that a machine neither rejects nor accepts an input x:
	- The machine loops on $x$.
- A TM is said to be total if it halts on all inputs 

# References

