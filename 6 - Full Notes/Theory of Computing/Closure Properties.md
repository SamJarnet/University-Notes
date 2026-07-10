28-10-2025 21:13

Status:

Tags: [[Theory of Computing]]


# Closure Properties

#### Helpful Proof
- Prove $\{a^nb^ma^nb^m|n, m \geq 0\}$ is not context free.
- PROOF:
	- 1. Demon picks some $k$
	- 2. We pick $z=a^kb^ka^kb^k$
	- 3. The demon has to pick strings $u,v,w,x,y$ such that $z=uvwxy, vx \neq \epsilon$ and $|vwx| \leq k$
	![[Pasted image 20251028212801.png]]
	- There are multiple choices for the demon in this step:
		- Either $v$ or $x$ contain both $a$'s and $b$'. Pick $i=2$, then the $uv^2wx^2y$ is not of the form $a^nb^ma^nb^m$ and so not in the language
		- $v$ and and $x$ contain only $a$'s. Pick $i=2$, then $uv^2wx^2$ will either be $a^lb^ka^kb^k$ or $a^kb^ka^lb^k$ with $l>k$, which is not in the language
		- Similar argument if $v$ and $x$ contain only $b$'s
		- $v$ contains only $a's$ and $x$ contains only $b$'s. Pick $i=2$, then $uv^2wx^2y$ will either be $a^lb^{l'}a^kb^k$ or $a^kb^ka^lb^{l'}$ with $l, l' > k$ - and this string is not in the language 
		- The language is not context free

#### Closure
- What does it mean that a class of languages is closed under a certain operation?
	- It means that if we take any languages from the class and apply this operation, we get a language that is still in the class.
- Example:
	- The class of CFLs is closed under union
		- If we take two CFLs $L_1$ and $L_2$, then $L_1 \cup L_2$ is still CF
- Example:
	- The class of CFLs is closed under concatenation
		- If we take two CFLs $L_1$ and $L_2$, then $L_1L_2$ is still CF
- Example:
	- The class of CFLs is closed under the Kleene star
		- If we take CFL $L_1$, then $(L_1)^*$ is still CF

- What does it mean that a class of languages is NOT closed under a certain operation?
	- It means that there exists some language from the class, such that, if we apply this operation, we obtain a language that is NOT in the class 
- Example:
	- The class of CFLs is NOT closed under complement
		- There are some CFLs $L_1$ such that their complement $(L_1)^c$ is NOT CF
- Note:
	- Not being closed under an operation, does NOT mean that, for all languages applying this operation gives us a language not in the class. It means that this happens at least for SOME language
- For instance:
	- There are some CFLs whose complement is still CF

#### Union
- CFLs are closed under union, i.e. for all CFLs $L_1$ and $L_2$, then $L_1 \cup L_2$ is a CFL
- Let $G_1 = (N_1, Σ_1, P_1, S_1)$  and $G_2 = (N_2, Σ_2, P_2, S_2)$ be the CFGs generating $L_1$ and $L_2$ respectively.
- Let  $G_3 = (N_3, Σ_3, P_3, S_3)$ be a CFG such that:
	- $\Sigma_3 = \Sigma_1 \cup \Sigma_2$ 
	- $N_3 = N_1 \cup N_2 \cup \{S_2\}$, where $S_3 \notin N_1 \cup N_2$ ($N_1$ and $N_2$ must be disjoint);
	- $P_3 = P_1 \cup P_2 \cup \{S_3 \rightarrow S_1, S_3 \rightarrow S_2 \}$;
	- Start variable: $S_3$
- It is clear that $L_1 \cup L_2 = L(G)$
- Example:
	![[Pasted image 20251029172400.png]]

#### Intersection with Regular Languages
- CFLs are closed under intersection with regular languages i.e.:
	- If $L_1$ is a CFL and $L_2$ is regular, then $L_1 \cap L_2$ is a CFL
- This can be used to prove a language is not context free:
	- Take a language $L_1$, you want to prove is not context-free and take a regular language $L_2$;
	- If their intersection $L_1 \cap L_2$ is not a context-free language, then $L_1$ could not have been context free to begin with.
- CFLs are not closed under intersection
- Consider:
	- $A_1 = \{ a^ n b^ n c ^m | n, m ≥ 0 \}$ and $A_2 = \{ a ^n b^ mc^ m | n, m ≥ 0\}$. Then these are CFLs 
	- Their intersection is $A_1 \cap A_2 = \{a^nb^nc^n | n \geq 0\}$
		- Which is not a CFL

#### Complement 
- CFLs are not closed under complement.
- For instance, the language $L=\{a, b\}^* - \{ww | w \in \{a, b\}^*\}$ is context free
- In fact there is a CFG for it:
	- $S → AB | BA | A | B$ 
	- $A → CAC | a$
	- $B → CBC | b$
	- $C → a | b$
- The complement of $L$ is
	- $L^c = \{ww | w \in \{a, b\}^*\}$
- Which we prove is not context free.
- We use intersection of $L^c$ with regular language $L(a^*b^*a^*b^*)$
- The result is language $\{a^nb^ma^nb^m|n, m \geq 0\}$
	- Which we showed is not context free
- So $L^c$ is not context free


# References