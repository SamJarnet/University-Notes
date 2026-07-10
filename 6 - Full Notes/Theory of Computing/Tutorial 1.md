29-09-2025 22:58

Status:

Tags:  [[Theory of Computing]]


# Tutorial 1

#### 1. Design a DFA over the alphabet {a, b} that accepts precisely the
- a) strings with an even number of ‘a’s. 
	![[Pasted image 20250929230312.png]]
- b) strings with an odd number of ‘a’s. 
    ![[Pasted image 20250929230331.png]]
- c) strings with number of ‘a’s divisible by 3. 
	![[Pasted image 20250929230554.png]]
- d) strings with number of ‘a’s divisible by n, for some n ∈ N. 
	![[Pasted image 20250929230756.png]]
- e) strings that either start with an ‘a’ and have odd length, or start with a ‘b’ and have even length.
	![[Pasted image 20250929231002.png]]


#### 2. a) Given a DFA M, how can we obtain a DFA M′ such that M′ accepts exactly those strings that are rejected by M?
- Switch start and final state

#### 2. b) Show that the class of regular languages is closed under complement. That is, if L is a regular language then so is ∼L = {x ∈ Σ ∗ | x /∈ L}.

#### 3. Prove the following: 
- a) ∅ and Σ∗ are regular languages
	![[Pasted image 20250930140357.png]]
- b) if $L_1$ and $L_2$ are regular then $L_1 \cup L_2$ is regular
	

# References