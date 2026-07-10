2026-05-07 17:46

Status:

Tags: [[Linear Temporal Logic]] [[Formal Specification and Verification]]


# Automata-Based Verification for LTL

#### Finite Automata over Infinite Words (Buchi Automata)
- An infinite run is an infinite path through the automaton starting in an initial state
- e.g. 
	![[Pasted image 20260507175217.png]]
- An automaton accepts an infinite word $a_1a_2a_4...$ if there exists a run of the automaton labelled by $a_1, a_2, ...,$ which passes through an accepting state infinitely often. We call such a run accepting.

#### Example
- The only initial state and only accepting state is $s_1$.
	![[Pasted image 20260507175444.png]]
- The run:
	![[Pasted image 20260507175456.png]]
	- is accepting
- The run:
	![[Pasted image 20260507175513.png]]
	- is not accepting
- The language of this Buchi automaton consists of all infinite words containing infinitely many $a$ symbols.

#### Properties of Buchi Automata 
- If $A$ and $B$ are automata, then there exists:
	- an automaton $A \cap B$ (the product automaton) such that $L(A \cap B) = L(A) \cap L(B)$
		- same construction as for finite automata works under suitable assumptions
	- an automaton $A^c$  (the complement automaton) such that $L(A^c)$ contains exactly those infinite words which are not in $L(A)$
		- not the same construction as for finite automata
		- Buchi automata cannot be determinised

#### From Transition Systems to Buchi Automata
- Transition systems can be transformed into Buchi automata, e.g.
	![[Pasted image 20260507180239.png]]
- automaton states correspond to transition system states, plus an additional initial state
- one transition from the new initial state to states that where initial in the transition system
- all other transitions come from the transition system
- the automaton alphabet is $P(Prop)$ (the set of all subsets of Prop)
- the labels on automaton transitions are inherited from target states in the transition system
- all automaton states are accepting
	- all runs are accepting.
- What is the language of the resulting automaton?
	- Exactly those infinite sequences of sets of atomic propositions along computation paths in the transition system.
	- For example:
		- atomic propositions: $Prop = \{n_1, n_2, t_1, t_2, c_1, c_2\}$
		- $\{n_1, n_2\} → \{t_1, n_2\} → \{c_1, n_2\} → \{n_1, n_2\} → . . .$ occurs along path through the transition system
		- $\{n_1, n_2\} , \{t_1, n_2\} , \{c_1, n_2\} , \{n_1, n_2\} , . . .$accepted by the automaton
	- Intuition: automaton runs correspond to transition system paths

#### LTL Model-Checking using Buchi Automata
- LTL formula involving Prop can also be transformed into an automaton over the alphabet $P(Prop)$.
- Intuition:
	- infinite words over P(Prop) describe sequences of sets of atomic propositions 
	- resulting automaton should accept an infinite word precisely when the corresponding sequence satisfies the given formula
- the model and the specification are both automata
	- we can use Buchi automata constructions for model-checking

#### From LTL to Buchi Automata (Mutual Exclusion)
- $A G \neg(c_1 ∧ c_2)$ becomes: 
	![[Pasted image 20260507181754.png]]
- Where:
	![[Pasted image 20260507181821.png|133]] stands for all arcs labelled by both $c_1$ and $c_2$:
	![[Pasted image 20260507181858.png]]
	![[Pasted image 20260507181918.png]] stands for all arcs labelled with subsets of Prop
	![[Pasted image 20260507181954.png]] stands for all arcs labelled with subsets of Prop not containing both $c_1$ and $c_2$

#### Example
- Mutual exclusion property $A G \neg(c_1 ∧ c_2)$ 
	![[Pasted image 20260507181754.png]]
	- Automaton accepts all infinite words not containing both $c_1$ and $c_2$ at the same time (i.e. within the same alphabet symbol).
- Liveness property $A F c_1$
	![[Pasted image 20260507182221.png]]
	- This automaton accepts all infinite words eventually containing $c_1$ as part of a symbol

#### LTL Model-Checking using Buchi Automata
- Model captured by Buchi automaton $A$
- specification (LTL formula) captured by Buchi automaton $S$
- Key observation:
	- model satisfies the specification iff $L(A) \subseteq L(S)$ (any behaviour in the model satisfies the specification)
- thus, checking property "$S$" on model "$A$" reduces to checking language inclusion $L(A) \subseteq L(S)$ 
- checking $L(A) \subseteq L(S)$ can be reduced to checking:
	- $L(A) \cap (L(S))^c = \emptyset$
- or equivalently 
	- 	- $L(A \cap S^c) = \emptyset$

- Need to compute automaton $A \cap S^c$ 
	- computing $A \cap B$ is relatively easy (polynomial complexity)
	- complexity of computing $S^c$ is exponential in the number of states, if $S$ is nondeterministic 
		- what if $S$ is deterministic
		- Note: not any non-deterministic Buchi automaton has an equivalent deterministic one 
	- better to generate automaton for negation of LTL property

#### Example
- automaton for negation of mutual exclusion property:
	![[Pasted image 20260507191640.png]]
- model automaton:
	![[Pasted image 20260507191656.png]]

#### Construction of the Product Automaton
- states of the product automaton given by pairs of states of the two automata 
- Note: only possible if all states of one automaton are accepting
	![[Pasted image 20260507191827.png]]
- $(s_1, s_2)$ is initial state precisely when both $s_1$ and $s_2$ are initial
- $(s_1, s_2)$ is accepting precisely when both $s_1$ and $s_2$ are accepting 

- Product automation has no accepting states, hence does not accept any infinite word:
	![[Pasted image 20260507192057.png]]
- Since the language of the product automaton is empty, the mutual exclusion property $AG \neg(c_1 ∧ c_2 )$ holds in the original transition system

- Automaton for negation of simple liveness property:
	![[Pasted image 20260507192203.png]]
- Model automaton:
	![[Pasted image 20260507192212.png]]
- Product automaton:
	![[Pasted image 20260507192227.png]]
- language accepted by the product automaton is not empty 
- so liveness property $AF c_1$ does not hold in the original model
- any infinite word accepted by above automaton is counterexample

#### LTL Model-Checking algorithm
- there is an algorithm which translates LTL formulas to Buchi automata 
- complexity of resulting model checking algorithm is linear in the size of the model and exponential in the length of the formula 
- fairness assumptions can be incorporated into LTL formulas

#### The SPIN model checker
- example of explicit state model checker
- uses Promela modelling language to describe concurrent/distributed software systems
- uses LTL as main mechanism for specifying correctness
- annotations to Promela models for simple safety/liveness properties
- can handle systems with millions of states

#### Benefits and Limitations of Explicit State Model Checking
- Benefits:
	- automatic
	- exhaustive
	- produces counter-examples
- Limitations:
	- state explosion problem - partially addressed by symbolic/bounded model checking 
	- only works for finite state systems

#### Beyond Model Checking
- Similar automata-based techniques can be used for software synthesis 
- the synthesis problem: given a specification, construct a (software) system which implements that specification 
	![[Pasted image 20260507193125.png]]
- specification is an LTL formula (or Buchi automaton) describing how outputs relate to inputs
- more complex than model checking



# References