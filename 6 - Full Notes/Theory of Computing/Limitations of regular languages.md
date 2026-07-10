13-10-2025 18:16

Status:

Tags: [[Theory of Computing]]


# Limitations of regular languages

#### Regular Languages
- The class of regular languages is quite robust:
	- It is the class of languages accepted by a family of finite automata, the class of languages matched by regular expressions 
	- It is closed under union, intersection, concatenation, Kleene star
- To prove a language is regular, we can either give a regular expression or a (non)deterministic automaton (with $\epsilon$-moves), or just use closure properties of RLs

#### Regular Languages
- Q: Are all languages regular?
- A: No. Prove using a counter argument:
	- Countably (~$N$) many regexps over $\sum$ 
	- Uncountably (~$2^N$) many languages over $\sum$ 
		- countably many strings over $\sum$
		- uncountably many sets of strings

#### Pumping
- Regular languages can be pumped
- Consider:
	- ![[Pasted image 20251013182249.png]]
- What happens if a string of length $4, 5, 6, ...$ is accepted? It has made a cycle which can be repeated any number of times!
	- e.g. $babba$ is accepted, and also $ba(bb)^na$ is accepted, for any $n \geq 0$; 
	- We say that the substring $bb$ can be pumped to generate new accepted strings.

#### A Non-Regular language
- $\{a^nb^n | n ∈ N\}$
- Rough idea:
	- Any DFA has finitely many states. To accept $a^{1000}b^{1000}$ and reject $a^{1000}b^{999}$ it has to be able to count the number of $a$'s and remember how many have been seen. Since the number is unbounded, there is no way to do this with a finite number of states.

#### Formal Proof
- Suppose that $M$ is an automaton that accepts $\{a^nb^n | n ∈ N\}$. Suppose that $M$ has $k$ states. Let $n > k$. Then $\exists q \in Q$ such that:
	- ![[Pasted image 20251013182908.png]]
- Then $M$ accepts also $a^{n-l}b^n$. Contradiction!

#### Pumping Lemma
- Suppose that $A$ is regular. There exists $k \in N$ such that for all strings $x,y,z$ with $xyz \in A$ and #$y \geq k$;
	- There exists $u, v, w$ with:
		- $y=uvw$ and $v \neq \epsilon$;
		- $xuv^iwz \in A$ for all $i \geq 0$.

#### Using the Pumping Lemma
- We will most often use the pumping lemma to show that a language is not regular
- The pumping lemma is of the form:
	- ($A$ regular) $\Rightarrow \Phi$ (1)
- This is logically equivalent to: 
	- $¬Φ \Rightarrow$ ($A$ is not regular) (2)
- (2) is the contrapositive of (1)
- To show that $A$ is not regular, it suffices to show $\neg \Phi$ 

#### Contrapositive Pumping Lemma
- If for all $k>0$, there exists strings $x,y,z$ so that $xyz \in A$ and #$y \geq k$ and:
	- For all strings $u, v, w$ with:
		- $y=uvw$ and $v \neq \epsilon$;
		- There exists  $i \geq 0$ such that $xuv^iwz \notin A$
	- Then $A$ is not regular
- The interplay between $∀$ and $∃$ can be understood as a game with an opponent
	- occurrences of $∀$ correspond to opponent moves
	- occurrences of $∃$ correspond to own moves

#### The Demon Game
- The game is played as follows: 
	1. Demon picks some $k > 0$; 
	2. we pick $x, y, z$ such that $xyz ∈ A$ and #$y ≥ k$; 
	3. demon picks $u, v,w$ such that $y = uvw$ and $v \neq \epsilon$ 
	4. we pick i ≥ 0 We win if $xuv^iwz \notin A$, the demon wins if $xuvi wz ∈ A$. 
- If we have a winning strategy (i.e. no matter what the demon picks, we can always win) then we have shown that A is not regular.

#### Example 1
- Let’s use the demon game to show that the following language is not regular: 
	- $A = \{a^nb^n | n ∈ N\}$
1. The demon picks some $k>0$ 
2. We pick $x=a^k, y=b^k, z=\epsilon$ then $xyz \in A$ (Check) and #$y \geq k$ (Check)
3. The demon picks some $u,v,w$ such that $y=uvw$ and $v \neq \epsilon$:
	- Because of our choice of $y, v = b^l$ for some $0 < l \leq k$ 
	- Then $u=b^r$ and $w=b^s$ for some $r, s \geq 0$ with $k=r+l+s$ (since $y=b^k=b^rb^lb^s$)
4. We pick $i=0$ 
	- Then $xuv^0wz=a^kb^rb^s \epsilon = a^kb^{r+s}=a^kb^{k-l}$ 
	- We win because $a^kb^{k-L} \notin A$ 
- This is a winning strategy because we have made no assumption on the demon choices: whatever the demon picks, we end up winning. Thus $A$ is not regular

#### Example 2 - Palindromes
- Let $\sum$ be an alphabet which contains at least two symbols, $a$ and $b$.
- We will show that the language $P$ of palindromes is not regular.  A palindrome is a string that reads equally left to right and from right to left.
- Assume $P$ is regular. Then also $P \cap L(a^*ba^*)$ is regular, since regular languages are closed under intersection. Clearly:
	- $P \cap L(a^*ba^*) = \{a^nba^n | n \in N \}$
- We play the demon game on $A  = \{a^nba^n | n \in N \}$
1. The demon picks some $k>0$ 
2. We pick $x=\epsilon, y=a^k, z=ba^k$ then $xyz = a^kba^k \in A$ (Check)
3. The demon divides $y$ into $uvw$ with $v \notin \epsilon$, hence $v=a^l$ for some $0 < l \leq k$
4. We pick $i=0$, clearly $a^{k-l}ba^k \notin A$ (Check)
- The above move is a winning strategy, and this $A$ is not regular

#### More Non-Regular Languages
- We know  $L = \{a^nb^n | n \geq 0\}$ is not regular.
- Q. How about $L' = \{w \in \{a, b\}^* | w \neq a^nb^n\}$?
	- A. $L'$ is not regular. If $L'$ was regular, then $L = \, \sim L'$ 
- Q. How about $L'' = \{a^nc^mb^n | n,m \geq 0\}$
	- A. $L''$ is not regular. If $L''$ was regular, then $L'' \cap L(a^*b^*)$ would also be regular. But $L'' \cap L(a^*b^*) = L$, which we know is know is not regular

# References