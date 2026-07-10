2025-11-24 15:03

Status:

Tags: [[Turing Machines]] [[Theory of Computing]]


# Non-Deterministic Turing Machines


#### Lessons Learnt
- $TIME(n)$ is not super-robust as a complexity class - whether $L \in TIME(n)$ depends on the choice of the computational model
- Having polynomial complexity is a robust property of languages - it does not depend on the choice of (deterministic) computation model


#### NTMs 
- A NTM is similar to a standard (deterministic) TM, except:
	- The machine can proceed according to several possible transitions (like an NFA)
	- The machine accepts an input if there exists and accepting computation for that input.
- Definition:
	-  An NTM is a tuple $M = (Q, Σ, Γ, ⊢, ⊔, δ, s, t,r)$ where:
		- $Q$ is a finite set of states,
		- $Σ$ is the input alphabet,
		- $Γ$ is the tape alphabet 
		- $⊔$ is the blank symbol,
		- $⊢∈ Γ$ \ $Σ$ is the left endmarker,
		- $δ : (Q$ \ $\{t,r\} × Γ →P(Q × Γ × \{L, R\})$ is the transition function, 
		- $s ∈ Q$ is the start state,
		- $t ∈ Q$is the accept state, 
		- $r ∈ Q$is the reject state, $r \neq t$.
- An NTM can be thought of as taking all possible transitions from a given configuration in parallel;
- The computation of an NTM is a tree:
	- Nodes are configurations, the start configuration is the root
	- Branches are individual computations
	- Leaves are accept/reject configurations
- Deterministic Machine:
	![[Pasted image 20251124204647.png]]
- Non-Deterministic Machine:
	![[Pasted image 20251124204715.png]].
- This is a non-physical model of computation

#### Definition
- An NTM:
	- Accepts an input if some branch of the computation tree leads to an accept configuration,
	- Rejects an input if all branches of the computation tree lead to a reject configuration.
- An NTM is a decider if all branches halt on all inputs
- Thus, an NTM accepts an input iff it can make a sequence of transition choices which result in accept configuration.
- Deciders are the non-deterministic equivalent of total TMs.
- A decider will either accept an input or reject it.

#### Expressiveness of NTMs 
- Theorem:
	- For any NTM $N$, there exists a DTM $D$ accepting for the same language
- Proof:
	- A NTM $N$ can be simulated by a multi-tape DTM $D$ which tries all branches of $N$s computation (breadth-first)
		- One tape stores input,
		- One tape used to simulate a branch up to a given depth,
		- One tape used to remember the branch being simulated.
		![[Pasted image 20251124205533.png]]
	- If $D$ reaches a reject state, it stops simulating that branch and continues with the next branch. If $D$ ever finds the accept state on one of the branches, it accepts. Otherwise $D$ will loop. So $L(D) = L(N)$. 
	- Corollary:
		- A language is recursively enumerable iff some NTM accepts it
- Note that $D$ does not reject the same inputs as $N$ (it never rejects)
- We cam modify $D$ so that it halts on an input, if all branches of $N$ halt on that input:
	- Remember the branches that halt (e.g. on a fourth tape);
	- Do not explore these branches again;
	- If there is no branch left to explore, reject.
- The modified $D$ now also rejects the same inputs $N$.
- Theorem: 
	- Any NTM has an equivalent DTM.
- If $N$ is a decider, then the modified $D$ is total.
- Corollary:
	- A language is recursive iff some NTM decides it 

#### Time Complexity of Deciders 
- Definition: 
	- The time complexity (or running time) of a decider $M$ is the function $f : \mathbb{N} \rightarrow \mathbb{N}$ where:
		- $f(n) =$ maximum number of steps $M$ uses on any branch of its computation, on an input of length $n$.
- Note:
	- The above definition does not correspond to any real-world computing device; we will use it later to define a class of problems


#### Comparing Computation Models
- Theorem:
	-  Let $t: \mathbb{N} \rightarrow \mathbb{N}$ be a function, where $t(n) \geq n$. Then every $t(n)$ time multi-tape Turing machine has an equivalent $O(t^2(n))$ time single-tape Turing machine.
- What about NTM to DTM?
- Theorem:
	- Let $t: \mathbb{N} \rightarrow \mathbb{N}$ be a function. Then every $t(n)$ time non-deterministic Turing machine has an equivalent $2^{O(t(n))}$ time DTM
- Note:
	- "$f(n)$ is $2^{O(t(n))}$" means $f(n) \leq 2^{c \, t(n)}$ for some constant $c > 0$ and all $n \geq n_0 \in \mathbb{N}$ fixed.

- Proof idea: Let $N$ be a $t(n)$ time NTM, and let $D$ be the equivalent multi-tape DTM.
- Since $N$ is a decider, $D$ is total. What is the time complexity of $D$?
	- 1. How many partial branches does $D$ have to simulate?
	- 2. How much time does it take to simulate a partial branch?
- For an input of length $n$:
	- Each branch of $N$ has length at most $t(n)$ 
	- Each node in $N$'s computation tree has up to $b$ children.
	- Hence there are at most $b^{t(n)}$ leaves, and $O(b^{t(n)})$ nodes/partial branches. 
- Total running time of $D: O(t(n) \times b^{t(n)})$, hence $2^{O(b^{t(n)})}$.
- Simulating this with a single-tape DTM requires:
	- $(2 ^{O(t(n))}) ^2 = 2^{ 2∗O(t(n))} = 2^{ O(t(n))}$ steps.
- NTMs are potentially more efficient than DTMs

# References