2025-10-29 18:12

Status:

Tags: [[The Shortest Path]] [[Nondeterminism and the Subset Construction]] [[Theory of Computing]]


# Pushdown Automata

#### Non-Deterministic Finite Automata 
- A way to look at an NFA:
	![[Pasted image 20251029181335.png]]
- Control represents states and transition function
- Tape contains the input string 
- Arrow is input head pointing at next input symbol

#### Pushdown Automata (PDA)
- We add: 
	![[Pasted image 20251029181443.png]]
- The control unit has access to memory: a stack
- The stack can hold unlimited amount of information
- At any time automaton can read and write (push) or remove (pop) symbols on stack

- $L=\{a^nb^n | n \geq 1\}$ is not regular, put there is a PDA that recognises it 
- How does this PDA work?
	- $a$ is read, push it on stack
	- $b$ is read, pop $a$ off stack
	- Finish reading input, stack empty of $a$s, final state reached, accept
	- Reject otherwise 

#### Formal Definition
- A pushdown automaton is a 7-tuple $(Q, \Sigma, \Gamma, \delta, s, ⊥, F)$ where $Q, \Sigma, \Gamma$ and $F$ are all finite sets and:
	- $Q$ is a set of states;
	- $\Sigma$ is the input alphabet;
	- $\Gamma$ is the stack alphabet;
	- $\delta$ is the transition relation
	- $s \in Q$ is the start state;
	- $⊥$ is the initial stack symbol;
	- $F \subseteq Q$ is the set of final states.

#### Transitions 
- $\delta$ is defined as:
	![[Pasted image 20251029182213.png]]
- $((q_i, w_i, a), (q_{i+1}, b_1...b_k))$ intuitively means:
	- In state $q_i$ read input $w_i$ and read $a$ on top of stack, then
	- pop $a$ off the stack, push $b_1...b_k$ on the stack and move to state $q_{i+1}$  $w_i, b_1...b_k$ can be $\epsilon$
	- $((q_i, \epsilon,a), (q_{i+1}, b_1...b_k))$ performs transition without reading any input 
	- $((q_i, w_i,a), (q_{i+1}, \epsilon))$  simply pops $a$ of the stack

#### Example:
- PDA that accepts the language $\{a^nb^n | n \geq 1\}$
- Let $\Sigma = \{a, b\}, \Gamma = \{a, ⊥\}, Q=\{0, 1, 2\}$ with $0$ the initial state and $2$ the final state;
	![[Pasted image 20251029191326.png]]
- Notation:
	![[Pasted image 20251029191416.png]]
- $\delta$ contains the following pairs:
	- $((0, a, ⊥), (0, a⊥))$     (1)
	- $((0, a, a), (0, aa))$         (2)
	- $((0, b, a), (1, ϵ))$             (3) 
	- $((1, b, a), (1, ϵ))$             (4)
	- $((1, ϵ, ⊥), (2, ϵ))$            (5)

- We want to define a notion of computation 
- A configuration describes the current state of the PDA, the con tent of the stack and the part of the input left to read 
- It is an element of:
	- $Q \times \Sigma^* \times \Gamma ^*$ 
- And has the form: 
	- $(q, w_1...w_k, v_1...v_m⊥)$
- Current state is $q$
- $w_1...w_k$ input left to read
- $v_1...v_m⊥$ symbols on stack top to bottom

#### Example: $(p, baaabba, ABAC⊥)$
![[Pasted image 20251029192139.png]]



#### Transitions and Configurations
- To define a notion of computation, we define a relation $\rightarrow$ between configurations;
- Let $w_1 ... w_k \in \Sigma ^*, bv_1...v_m \in \Gamma ^*$, we write
	- $(q, w_1...w_k, bv_1...v_m⊥) \rightarrow (q', w_2...w_k, av_1...v_m⊥)$
- Whenever:
	- $((q, w_1, b), (q', a))$
- We are in state $q$, read $w_1, b$ is on top of the stack
- We move to $q'$, pop $b$ of the stack and put $a$ on
- $w_2...w_k$ is remaining input
- $av_1...v_m⊥$ is stack from top to bottom

#### Accepting Computation
- Given configurations $C_1, C_2$ we say here is a computation of $C_2$ from $C_1$, denoted $C_1 \Rightarrow C_2$, if there exists configurations $C'_1, ..., C'_k$ for some $k \in N$ such that
	- $C_1 \rightarrow C'_1 \rightarrow ... \rightarrow C'_k \rightarrow C_2$ 
- Computations for PDAs start from an initial configuration
	- $(s, w_1...w_k,⊥)$
- $w=w_1...w_k \in \Sigma ^*$ is accepted by a pushdown automaton if there exists $q' \in F$ such that 
	- $(s, w_1...w_k,⊥) \Rightarrow (q', \epsilon, v)$
- Acceptance means there is a computation from start configuration to a configuration with final state where all input is consumed 

#### Language Recognition
- Let $M = (Q, Σ, Γ, δ,s, ⊥, F)$ be a pushdown automaton
	- $L(M) = \{w | w ∈ Σ ∗ , ∃q ∈ F$ such that $(s, w, ⊥) ⇒ (q, ϵ, v)\}$
- $L(M)$ is the language recognised by the pushdown automaton $M$.
- The class of context-free languages is the class of languages recognised by pushdown automata
- Example:
	- Acceptance of $aaabbb$: 
	![[Pasted image 20251104220942.png]]

#### Acceptance by Empty Stack
- By definition, a PDA accepts a string $w$ when there exists $f \in F$ such that:
	- $(s, w, ⊥) \Rightarrow (f, \epsilon, g)$ 
- This is acceptance by final state 
- Another possible definition: $M$ accepts $x$ if there exists some $q \in Q$ such that:
	- $(s, w, ⊥) \Rightarrow (q, \epsilon, \epsilon)$ 
- This is acceptance by empty stack
- The two notions can be show to be equivalent i.e.:
	- Any PDA $M$ that accepts by final state can be made into a PDA $M'$ that accepts by empty stack.
	- Any PDA $M$ that accepts by empty stack can be made into a PDA $M'$ that accepts by final state.





# References