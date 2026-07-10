29-09-2025 15:00

Status:

Tags: [[Theory of Computing]]


# Automata Theory

Source code -> Lexical Analysis (RegExp, FA) -> lexical tokens -> Parsing (CFG, PDA)-> abstract syntax

#### Preview
- Finite automata are machines which accept / reject strings
- They describe languages (sets of strings)
- Regular expressions are another formalism for this
#### Alphabets & strings 
- An alphabet Σ is any finite set (of symbols)
	- e.g. {0, 1}, {a, b, c}, {a, b, . . . , z}, {0, 1,..., 9, +, ×} 
- A string over Σ is a finite sequence of symbols in Σ 
	- e.g. 0100101, abba, 21 + 37 
- The length # of a string is the number of symbols it contains 
		- e.g. #(abba)=4 
- The empty string $\in$  is a string, #($\in$)=0
#### Properties of Strings
- Two strings ${s, t}$ are equal when they contain the same letters in the same order
- The set if all strings over is denoted as ${\sum *}$
- Every string is either empty (${\in}$) or of the form ${x σ}$ where $σ \in \sum$
- "length" is then a function # : $\sum ^{*} \rightarrow \mathbb{N}$ where $\mathbb{N}$ is a set of natural numbers {0, 1 , ... }. We can define it using recursion:
	-  #$(\in) = 0$, #$(xσ)$ = #$(x) + 1$ 

#### Concatenation
- Given two strings $s, t \in \sum *$, their concatenation is denoted $st$
	- e.g. if $s=abb, t=ba$ then 
		- $st = abbba, ts = baabb, tst = baabbba$ 
	- any string $t$ satisfies the property that $\in$$t$ $=$ $t$$\in$ $= t$ 
- We write $a^n$ for a string containing $n$ copies of $a$:
	- $a^0 = \in, a^{n+1} = a^{n}a$ 

#### Languages 
- Given alphabet $\sum$, the set of all strings over $\sum$ is denoted $\sum ^*$ .
- Therefore, a language over $\sum$ is a subset of $\sum ^*$ .
	- e.g. $\sum = 0, 1: L_1 = \{1\}, L_2 = \{10^k | k \geq 0\}, L_3 = \sum ^*$ are languages over $\sum$
	- e.g. ${\sum = \{0, . . . , 9\} \cup \{+, -, .\}: L = \{s \in \sum ^* | s}$ is a valid decimal number $\}$ is a language over $\sum$ 
	- Two languages are equal when they contain the same strings (i.e. they are equal as sets)

#### Languages examples
- Let $\sum = \{a, b, c \}$.
	- $L_1 = \{a^n | n \in \mathbb{N}\}$ 
	- $L_2 = \{a^n | n \in \mathbb{N}$ is even $\}$  
	- $L_3 = \{{a^n}{b^n} | n \in \mathbb{N}\}$ 
	- $L_4 = \{{a^n}{b^n}{c^n} | n \in \mathbb{N}\}$ 
- More languages (over other alphabets):
	- $L_5 = \{e | e$ is a well=formed arithmetic expression $\}$ 
	- $L_6 = \{e | e$ is a syntactically correct C program $\}$ 

#### Finite automata
- Finite automata algorithmically decide if a string belongs to it or not
	- Used in text processing, compilers, hardware design

#### Machines with state
- State - a description of a system at some point in time
- Finite automata are systems with a finite number of states
- Three variants of finite automata:
	- Deterministic, nondeterministic and nondeterministic with $\in$-moves 

#### A deterministic finite automation
![[Pasted image 20250929185449.png]]
- This above picture of a DFA over the alphabet $\{a, b\}$ with two states, 0 and 1;
- The arrows, labelled by symbols, represent transitions, i.e. allowed moves;
- 0 is a start state;
- 1 is a final state.

#### Deterministic acceptance
- An automaton accepts some strings (and rejects those that is doesn't accept)
- Diagrammatically: place a pebble on the initial state, move it according to the symbols in the input string. Accept if at the end the pebble is on the final state, otherwise reject.
	- Accepted:
		- abbab
		- babbbab
	- Rejected:
		- abba

#### DFAs, formally 
- a DFA $M = (Q, \sum, \delta, s, F)$ 
	- $Q$ is a finite set of states;
	- $\sum$ is an alphabet;
	- $\delta : Q \times \sum \rightarrow Q$ is the transition function;
		- we will write $q \xrightarrow{a} q'$ for $\delta (q, a) = q'$;
	- $s \in Q$ is the start state;
	- $F ⊆ Q$ is the set of final states;

#### Picture formal resentation
![[Pasted image 20250929222232.png]]

#### Deterministic acceptance
- An automaton accepts some strings (and rejects those that it doesn't accept)
- For $\sigma _1, \sigma _2 \in \sum$, write $q \xrightarrow{\sigma _1, \sigma _2} q'$ when there is a $q''$ such that  $q \xrightarrow{\sigma _1} q''$ and $q'' \xrightarrow{\sigma _1} q'$. Similarly for longer strings. Write $q \xrightarrow{\in} q''$ when $q = q'$  
- Claim: any string $x \in \sum ^*$ determines a unique state $q$ such that $s \xrightarrow{x} q$ 
- $M$ accepts $x$ when q $\in F$ 
#### Regular languages
- For a DFA $M = (Q, \sum, \delta, s, F)$, its language $L(M)$ is the set of all strings accepted by $M$:
	- $L(M) = \{x \in \sum ^* | ∃f \in F. s \xrightarrow{x} f\}$ 
- A language is regular when $L(M)$ for some DFA $M$.

#### Designing DFAs
- Task: design a DFA over the alphabet {0, 1} for the following languages 
	- L = {w | w contains an even number of 0s } 
		- ![[Pasted image 20250929224516.png]]
	- {w | w contains at least two consecutive 0s}
		- ![[Pasted image 20250929224449.png]]
	- {w | w starts with 0 and has odd length, or starts with 1 and has even length}
		- ![[Pasted image 20250929224959.png]]

#### Closure properties
- Fix an alphabet $\sum$.
	- $\emptyset$ and $\sum ^*$ are regular;
	- if $L$ is regular then the component $\sum ^{*} - L$ (sometimes written $\sim L$) $= \{ x \in \sum ^* | x \notin L\}$ is regular;
	- if $L_1$ and $L_2$ are regular then $L_1 \cup L_2$ is regular;
	- if $L_1$ and $L_2$ are regular then $L_1 \cap L_2$ is regular;
	-  if $L_1$ and $L_2$ are regular then their concatenation $L_{1}L_2 = \{xy | x \in L_1, y\in L_2\}$;
	- if $L$ is regular then its Kleene Star $L^* = \{x_1 . . . x_k | k \in \mathbb{N}, x_i \in L \}$

#### Properties of automata
- The product construction is useful for providing some of the properties on the previous slide
- Intuition: if $M_1$ and $M_2$ are DFAs over $\sum$, then $M_1 \times M_2$ is the DFA that simulates running $M_1$ and $M_2$ in parallel.
	![[Pasted image 20250930135359.png]]

#### The product construction
- Formally: given $M_1 = (Q_1, \sum, \delta _1, s_1, F_1)$ and $M_2 = (Q_2, \sum, \delta _2, s_2, F_2)$ let $M_3$ be defined:
	- $Q_3 = Q_1 \times Q_2$ 
	- $\delta _3 ((q_1, q_2), \sigma) = (\delta (q_1, \sigma), \delta _2 (q_2, \sigma))$ 
	- $s_3 = (s_1, s_2)$ 
	- $F_3 = F_1 \times F_2$ 
- Claim: $L(M_3) = L(M_1) \times L(M_2)$
# References