2025-11-24 13:40

Status:

Tags: [[Turing Machines ]] [[Theory of Computing]]


# Time Complexity Of Turing Machines

#### From Computability to Complexity
- Computability classifies problems into:
	- 1. Those which are solvable by a computable (decidable)
	- 2. Those which are not 
- From now on we focus on decidable problems
- Even when a problem is solvable in principle, it may not be solvable in practice, if the solution requires too much time/memory
	- e.g. scheduling problems
- Complexity theory classifies decidable problems according to the amount of resources required to solve them.

#### Complexity Classes
- We have tools to measure:
	- The size of the input to an algorithm (length of input string)
	- The amount of time an algorithm takes (number of steps the TM takes)
	- The amount of (additional) space required (number of cells the TM uses)
- Some complexity classes:
	- P (Polynomial time), EXPTIME (Exponential time), ...
	- PSPACE (Polynomial space), EXPSPACE (Exponential space), ...

#### Terminology
 - A problem:
	 - A computational problem with a set of possible input and prescribed corresponding outputs
		 - e.g. sorting a list of integers
- An algorithm:
	- A procedure for solving a problem
		- e.g. merge sort 
- A problem instance:
	- A possible input to a given problem
		- e.g. the list "21 8 14 3 35"

#### Decision Problems
- A computational problem is called a decision problem if the output for any problem instance is either "yes" or "no"
- Problem instances are classified into positive/"yes" instances and negative/"no" instances.
- Examples:
	- Is a given number prime?
	- Does a given graph admit a Hamiltonian path?
	- Is a given string a syntactically correct C program?

#### From Decision Problems to Languages
- Given a decision problem $D$:
	- We can encode problem instances as strings over an alphabet $\Sigma$;
	- Then the "yes" instances of $D$ give rise to a language over $\Sigma$:
		- $L_D = \{w \in \Sigma^* | w$ encodes a "yes" instance of $D\}$
	- Solving D is equivalent to deciding $L_D$. 

#### Why Complexity Classes? Time Complexity and Machine Speed
- Let $D$ be a decision problem. Suppose we can solve a size $n$ problem in 1 hour. IF we double the machine speed how big of a problem can we now solve in 1 hour?
	![[Pasted image 20251124135417.png]]
- Key observations:
	- The lower the complexity, the greater the gain
	- Improvement is significant for polynomial (or better) complexity, but insignificant for exponential complexity

#### Time Complexity of Turing Machines
- Definition:
	- Let $M$ be a deterministic Turing machine which halts on all inputs.
- The time complexity (or running time) of $M$ is the function $f:\mathbb{N} \rightarrow \mathbb{N}$ where $f(n)$ = maximum number of steps $M$ uses on an input of length $n$.
- We say that $M$ is an $f(n)$ time Turing machine

#### Measuring Time Complexity (Example 1)
- Turing Machine $M_1$ for language $L = \{0 ^k1^ k | k ≥ 0\}$:
- On input $w \in \{0, 1\}^*$: 
	- 1. Scan across tape and reject if $w$ is not of the form $0^*1^*$.
	- 2. Repeat if both 0s and 1s remain on the tape:
		- 3. Scan across tape crossing off a single 0 and a single 1
	- 4. If 0s still remain after all 1s are crossed off, or if 1s still remain after all 0s are crossed off, reject. Otherwise accept.
- Clearly, $L(M_1) = L$ 

#### Big-O Notation
- Let $f, g : \mathbb{N} \rightarrow \mathbb{R}^+$.
- We say that $f(n)$ is $O(g(n))$ if 
	- There exist real $c > 0$, integer $n_0 > 0$ with 
		- $f(n) \leq c \, g(n)$ for all $n \geq n_0$ 
- We call $g(n)$ an asymptotic upper bound for $f(n)$ 
- Examples: 
	- $2n+1 = O(n^2)$,   $nlog(n) = O(n^2)$,   $(n-1)^2 = O(n^2)$ 
- Intuition: $f(n) = O(g(n))$ means "asymptotically $f \leq g$"

#### Little -O Notation
- Let $f, g : \mathbb{N} \rightarrow \mathbb{R}^+$.
- We say that $f(n)$ is $o(g(n))$ if 
	- $n \xrightarrow{lim} ∞ \frac{f(n)}{g(n)} = 0$ 
- We call $g(n)$ a strict asymptotic upper bound for $f(n)$ 
- Examples: 
	- $√ n = o(n)$,   $nlog(n) = o(n^2)$,   $(n-1)^2$ is not  $O(n^2)$ 
- Intuition: $f(n) = o(g(n))$ means "asymptotically $f < g$"


#### Example 1 Continued
- Upper bound on number of steps needed on input size n:
	![[Pasted image 20251124141323.png]]
- Total time for $M_1$ on input size $n$ is $O(n^2)$.

#### The complexity Class TIME(t(n))
- Definition:
	- Let $t: \mathbb{N} \rightarrow \mathbb{R}^+$ be a function. The time complexity class TIME(t(n)) is the collection of all languages that are decidable by an $O(t(n))$ time Turing machine.
- So $L \in TIME(n^2)$
- Can we do better than $M_1$ for deciding $L$?
	- Is $L \in TIME(f(n))$  for $f(n) = o(n^2)$ 

#### Measuring Time Complexity (Example 2)
- Turing Machine $M_2$ for language $L = \{0 ^k1^ k | k ≥ 0\}$:
	- 1. Scan across tape and reject if $w$ is not of the form $0^*1^*$.
	- 2. Repeat if both 0s and 1s remain on the tape:
		- 3. Scan across the tape, checking if the total number of 0s and 1s remaining is even or odd. If odd, reject
		- 4. Scan across the tape, crossing off every other 0 starting with the first 0, and every other 1 starting with the first 1
	- 5. If no 0s and no 1s remain on the tape, accept. Otherwise, reject.
- Upper bound on number of steps needed on input size n:
	![[Pasted image 20251124142925.png]]
- Total time for $M_2$ on input size $n$ is $O(nlogn(n))$. So $L \in TIME(nlog(n))$


Measuring Time Complexity (Example 3)
- Two-Tape Turing Machine $M_3$ for language $L = \{0 ^k1^ k | k ≥ 0\}$:
	- 1. Scan across tape and reject if $w$ is not of the form $0^*1^*$.
	- 2. Scan across the 0s on tape 1 until the first 1. At the same time, copy the 0s onto tape 2.
	- 3. Scan across the 1s on tape 1 until the end of the input. For each 1 read on tape 1, cross off a 0 on tape 2. If all 0s are crossed off before all the 1s are read, reject.
	- 4. If all the 0s have now been crossed off, accept. If any 0s remain, reject.
- Upper bound on number of steps needed on input size n:
	![[Pasted image 20251124143304.png]]
- Total time for $M_2$ on input size $n$ is $O(n)$. So $L \in TIME(n)$

- Observations:
	- Cannot do better for $L$ than $TIME(n)$ - must read entire input before deciding 
	- To show $L \in TIME(n)$, we had to change the computation model.
		- Choice of computational model affects the time complexity of a language.

#### Comparing Computational Models
- Theorem:
	-  Let $t: \mathbb{N} \rightarrow \mathbb{R}^+$ be a function, where $t(n) \geq n$. Then every $t(n)$ time multi-tape Turing machine has an equivalent $O(t^2(n))$ time single-tape Turing machine.
- Proof idea:
	- Any $k$-type TM $M$ can be simulated by a single-tape TM $M'$:
		- tape of $M'$ structured into tracks,
		- special markers used by $M'$ to identify tape heads,
		- $M'$ starts by copying the input onto its 1st track
		- to simulate a single step of $M$, $M'$ must:
			- find positions of tape heads and read symbols at those positions,
			- update the tape contents and head positions
	- Show that $M$' runs in $O(t^2(n))$ time:
		- If $M$ runs in $t(n)$ time, it can only use $t(n)$ tape cells on each tape.  Hence $M'$ also uses at most $t(n)$ tape cells. 
		- Copying the input to the first track needs $O(n)$ steps. $M'$ needs to simulate all steps of $M$; there are at most $t(n)$ steps. 
		- Simulating a single step of $M$ needs $O(t(n))$ steps 
			- One pass through the tape needed to find tape heads and read symbols,
			- One pass needed to update tape contents and head markers
		- In total, $M'$ needs $O(n) + t(n) \times O(t(n)) = O(t^2(n))$ steps 

# References