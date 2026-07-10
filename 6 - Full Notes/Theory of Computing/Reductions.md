2025-11-17 21:13

Status:

Tags: [[Theory of Computing]] [[Turing Machines]]


# Reductions

#### Undecidability 
- We showed that HP is undecidable.
- We can use a technique called reduction to prove some sets are not recursive/recursively enumerable 
- Example: Can we decide, given any TM $M$ as input, whether $M$ accepts $\epsilon$?
	- i.e. is $A = \{M | \epsilon \in L(M)\}$ a recursive set?
- No: We will see that we cam reduce HP to it.
	- "$HP \leq A$"

#### An Undecidable Problem
- We show that $A = \{M | \epsilon \in L(M)\}$ is not recursive.
- In fact, if we could decide $A$, then we would be able to decide $HP$.
- Take a TM $M$ and string $x$. Suppose we wish to determine whether $M$ halts on $x$.
- Construct from $M$ and $x$ a new TM $M'$ that does the following on input $y$.
	- Erases $y$;
	- Writes $x$ on its tape;
	- Runs $M$ on $x$;
	- Accepts if $M$ halts on $x$.
	![[Pasted image 20251117212345.png]]
- If $M$ halts on $x$, then $M'$ accepts $y$
- If $M$ does not halt on $x$, then $M'$ does not accept $y$
- Then, for every $y$
	![[Pasted image 20251117212558.png]]
- We can use the above to show that $A = \{M | \epsilon \in L(M)\}$  is not recursive.
- Suppose we could decide whether a TM accepts $\epsilon$, then we could apply this to $M'$ and decide HP.
- In fact, given $M$ and $x$, build $M'$ as above, then
	- $\epsilon \in L(M')$ $\Leftarrow \Rightarrow$ $M$ halts on $x$
- We have reduced HP to $A$ 

#### Reduction, Formally 
- A function $f:\Sigma^* \rightarrow \Delta ^*$ is computable when there exists a total TM $K$ that when started with $x \in \Sigma ^*$ on its tape, eventually halts with $f(x) \in \Delta ^*$ on its tape; 
- A reduction of $A \subseteq \Sigma ^*$ to $B \subseteq \Delta ^*$ is a computable function $f:\Sigma^* \rightarrow \Delta ^*$ s.t. 
	- $x \in A \Leftarrow \Rightarrow f(x) \in B$ 
		![[Pasted image 20251117233434.png]]
- We write $A \leq B$ if $A$ is reducible to $B$.

#### Properties of Reductions
- Theorem:
	- If $A \leq B$ and $B$ is r.e. then so is $A$. Equivalently, if $A$ is not r.e. then $B$ is not r.e. 
	- If $A \leq B$ and $B$ is recursive then so is $A$. Equivalently, if $A$ isn't recursive then neither is $B$.
- Proof:
	- 1. If $A \leq B$ then there is a computable function $f$ such that
		- $f(x) \in B \Leftarrow \Rightarrow x \in A$ 
	- If $B$ is r.e. then there is a TM $M$ that accepts it.
	- The following is a TM $K$ for $A$: on $x$, first compute $f(x)$, then run $M$ on $f(x)$, accepts if it accepts 
		- $x ∈ L(K) ⇒ f (x) ∈ L(M) ⇒ f (x) ∈ B ⇒ x ∈ A$ 
		- $x ∈ A ⇒ f (x) ∈ B ⇒ f (x) ∈ L(M) ⇒ x ∈ L(K)$
	- 2. Suppose $A \leq b$ and $B$ is recursive. Note that $A^c \leq B^c$:
		- $x ∈ A^ c ⇒ x \notin A ⇒ f (x) \notin B ⇒ f (x) ∈ B ^c$
		- $f (x) ∈ B ^c ⇒ f (x) \notin B ⇒ x \notin A ⇒ x ∈ A^ c$
	- Now $B$ is recursive, so both $B$, $B^c$ are r.e., and so both $A$, $A^c$ are r.e. and $A$ is recursive
#### Example 1
- The set $MP = \{M$#$x | x ∈ L(M)\}$ is not recursive (MP is known as the membership problem)
- We show that there is a reduction of HP to MP: HP $\leq$ MP. 
- We show that HP is not recursive, so, by the above theorem, MP is not recursive either.
- To obtain a reduction, we give a computable map $f$ such that 
	- $M$#$x ∈ HP ⇔ f (M$#$x) ∈ MP$
	![[Pasted image 20251119213230.png]]
- From $M\#x$ we want to construct a machine $M' = f(M\#x)$ such that 
	- $M$ halts on $x$ $⇔$ $M'$ accepts $x$
- Given $M\#x$, construct a machine $M'$ such that is like $M$ but with a new accept state and transitions from old accept and reject states to a new accept state. So whenever $M$ accepts or rejects, $M'$ accepts.
- If $M$ halts on $x$, then $M'$ accepts $x$.
- If $M$ does not halt on $x$, then $M'$ does not accept $x$.
- Then 
	- $M$ halts on $x$ $\Rightarrow$ $x \in L(M')$ 
	- $M$ does not halt on $x$ $\Rightarrow$ $x \notin L(M')$ 
- We have a reduced HP to MP, and so proved that MP is not recursive.

#### Example 2
- The set FIN $= \{M | L(M)$ is finite $\}$ is not r.e.
- The key idea is to reduce $HP^c$ to FIN: HP$^c$ $\leq$ FIN.
- HP$^c$ is not r.e., so, by the above theorem, FIN is not recursively enumerable either.
- To obtain a reduction, we give a computable map $f$ such that 
	- $M$#$x ∈ HP ⇔ f (M$#$x) ∈ FIN$
	![[Pasted image 20251119213230.png]]
- From $M\#x$ we want to construct a machine $M' = f(M\#x)$ such that 
	- $M$ does not halt on $x$ $⇔$ $L(M')$
- $M'$ will depend on $M$ and $x$ 
- Given $M\#x$, construct $M'$ such that on all inputs $y$:
	- (1) erases $y$; (2) writes $x$ on its tape; (3) runs $M$ on $x$; (4) accepts if $M$ halts on $x$.
- If $M$ does not halt on $x$, then simulation in (3) never halts, and $M'$ does not accept $y$, for all inputs $y$, therefore $L(M') = \emptyset$.
- If $M$ halts on $x$, then simulations in (3) halts, $M'$ accepts $y$ for all $y: L(M') = \Sigma ^*$.
- Then 
	- M halts on $x$ $\Rightarrow$ $L(M') = \Sigma ^*$ $\Rightarrow$ $L(M')$ is infinite
	- M does not halt on $x$ $\Rightarrow$ $L(M') = \emptyset$ $\Rightarrow$ $L(M')$ is finite
- We have a reduced HP$^c$ to FIN, and so proved that FIN is not recursively enumerable.

[[Decidable Problems]]
# References