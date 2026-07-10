07-10-2025 18:25

Status:

Tags: [[Theory of Computing]]


# Regular Expressions and Kleene's Theorem

#### Closure Properties of RLs
- The class of regular languages is closed under:
	- Union
	- Intersection
	- Complement
	- Concatenation: $L_{1}L_2 = \{xy | x ∈ L_1, y ∈ L_2\}$
	- Kleene Star: $L^∗ = \{x_1 ...x_k | k ∈ \mathbb{N}, x_i ∈ L\}$ 

#### Regular Expressions, I
- Given an alphabet $\sum$, the set of of regular expressions over $\sum$ is defined inductively.
- Base cases:
	- Every $\sigma \in \sum$ is a regular expression
		- $L(\sigma) = \{\sigma\}$ 
	- $\epsilon$ is a reg. exp
		- $L(\epsilon) = {\epsilon}$ 
	- $\emptyset$ is a reg. exp
		- $L(\emptyset) = {\emptyset}$

#### Regular expressions, II
- Operations
	- If $\alpha , \beta$ are reg. exp. then $\alpha + \beta$ is a regular expression
		- $L(α + β)= L(α) ∪ L(β)$
		- Some authors write $α | β$ instead of $α + β$ 
	- If $\alpha , \beta$ are regular expressions then $\alpha \beta$ is a regular expression
		-  $L(α  β)= L(α)  L(β)$
	- If $\alpha$ is a regular expression then $\alpha ^ *$ is a regular expression 
		- $L(α^∗) = L(α)^∗$
	- Precedence order: $^*$, then concatenation, then $+$

#### Examples:
- We say that a string $s$ matches a regular expression $\alpha$ whenever $s \in L(\alpha)$.
- For $\sum = \{a, b\}$
	- No strings match $\emptyset$ (since $L(\emptyset) = \emptyset$);
	- Strings that end in $b$ match $(a + b)^{∗}b$;
	- $L((a + b) ^{∗} b) = L((a + b) ^{∗} )L(b)$  $= L(a + b) ^{∗} L(b) = (L(a) ∪ L(b))^{∗} {b} = {a, b}^{∗} {b} = {x_1 ...x_{n}y | n ∈ N, x_i ∈ {a, b}, y ∈ {b}}$
	- strings of even length match $((a+b)(a+b))^*$;
	- $abba$ and the empty string match $abba + \epsilon$ 

#### Regular Expressions in compiler design
- The following regular expression over the alphabet $\{+, -, ., 0, 1, . . . , 9\}$ describes numerical constants:
	- $(+ \+ - \+ \epsilon)(dd^* \+ dd^*.d^* \+ .dd^*)$  
- where
	- $d:= 0+1+...+ 9$ 
- The following strings match this regular expression: $12, -3, 1.5, +.7$ 
- ![[Pasted image 20251007190908.png]]

#### Exercise:
- {w ∈ {a, b}∗ | every b in w is immediately followed by an a }
- $(a + ba)*$ 
- ![[Pasted image 20251007192418.png]]

#### Kleene's Theorem
- Theorem. 
	- If $α$ is a regexp then $L(α)$ is a regular language
	- If L is a regular language then $L = L(α)$ for some regexp $α$
- In other words, finite automata and regular expressions describe the same languages!

#### Proving Kleene's Theorem
- We know that DFAs, NFAs and $\epsilon$NFAs accept precisely the regular languages;
- To prove Kleene's theorem we will:
	- 1. Show how to convert a regex to a $\epsilon$NFA for the same language;
	- 2. Show how to convert any NFA to a regular expression to the same language

#### Reg Exp to Finite Automation
- The set of regular expressions is built inductively:
	- $\sigma \in \sum, \epsilon$ and $\emptyset$ are the base cases;
	- $+$, concatenation and $-^*$ are the operations 
- So to prove that $\forall \alpha . L(\alpha)$ is regular we need to prove that:
	- $L(\sigma), L(\epsilon)$ and $L(\emptyset)$ are regular
	- If $L(α), L(β)$ are regular then so is $L(α + β)$; 
	- if$ $L(α), L(β$) are regular then so is $L(αβ)$;
	- if $L(α)$ is regular then so is $L(α∗)$.

#### Base Cases
- $L(σ) = \{σ\}$ is regular; 
	- ![[Pasted image 20251008151059.png]]
- $L\epsilon!) = \{\epsilon \}$ is regular;
	- ![[Pasted image 20251008151152.png]]
- $L(∅)  = ∅$ is regular;
	- ![[Pasted image 20251008151216.png]]

#### Plus
- Want to show that $L(α + β) = L(α) ∪ L(β)$  is regular;
- Can assume $L(\alpha)$ and $L(\beta)$ are regular;
- We already proved that regular languages are closed under union. Hence $L(\alpha + \beta)$ is regular.
#### Concatenation
- Want to show that $L(\alpha \beta) = L(\alpha)L(\beta)$ is regular;
- Can assume $L(\alpha)$ and $L(\beta)$ are regular;
- We already proved that regular languages are closed under concatenation. Hence $L(\alpha \beta)$ is regular.

#### Kleene Star
- Want to show that $L(\alpha ^*) = L(\alpha)^*$ is regular;
- Can assume $L(\alpha)$ is regular;
- Let $M$ be an NFA for $L(\alpha)$. We construct a new $\epsilon$NFA $M'$:
	- ![[Pasted image 20251008151813.png]]
	- New initial state 0;
	- as transitions of $M'$ take those of $M$ plus $\epsilon$-transitions as above;
	- as final states of $M'$ take the singleton {0}.
- It is easy to show that:
	- $L(M') = L(M)^* = L(\alpha)^* = L(\alpha ^*)$


#### Exercise
- $(a^*b)^*$
- ![[Pasted image 20251008160527.png]]
  


# References