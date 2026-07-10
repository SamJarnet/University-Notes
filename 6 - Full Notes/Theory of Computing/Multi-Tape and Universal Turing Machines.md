2025-11-11 13:17

Status:

Tags: [[Theory of Computing]] [[Turing Machines]]


# Multi-Tape and Universal Turing Machines

#### Multi-Tape Turing Machines
- We show that multi-tape TMs can be simulated by single-tape TMs, so their expressive power is the same.
- We focus on three-tape TMs, but the construction can be easily generalised.
- A three-tape TM has three semi-infinite tapes and three independent read/write heads:
	![[Pasted image 20251111132049.png]]
- Input is initially on first tape and others are blank.
- At each step, machine reads symbols under each head, and, depending on current state, moves each head independently and enters new state.

- Transition function is of type:
	- $\delta : Q \times \Gamma^3 \rightarrow Q \times \Gamma^3 \times \{L, R\}^3$ 
- For example, $δ(p, (a, b, b)) = (q, (b, b, a), (L, R, L))$ means that, in state $p$ (simultaneously)
	- Head 1 reads $a$, writes $b$ and moves left
	- Head 2 reads $b$, writes  and moves right
	- Head 3 reads $b$, writes $a$ and moves left
- Machine moves to state $q$ 
	![[Pasted image 20251111132520.png]]
	![[Pasted image 20251111132745.png]]

- We build a single-tape TM $N$ that simulates a three-tape TM $M$
- $N$ has expanded tape-alphabet that includes symbols of the form
	![[Pasted image 20251111132853.png]]
- Where $c,d,e$ are symbols of $M$.
- These symbols can be marked, i.e. $\hat{c}$ or unmarked, i.e. $c$.
- Marked symbols simulates position of $M$'s heads

- Formally the tape alphabet has the following form:
	- $\Sigma \cup \{⊢\} \cup (\Gamma \cup \Gamma')^3$
- With:
	- $\Gamma' = \{\hat{c} | c \in \Gamma \}$
- The three elements of $(\Gamma \cup \Gamma')$ encode symbols in same position on $M$'s tapes.
- You can think of $N$ as having three tracks on same tape simulating the tapes of $M$
- Blank symbol is:
	![[Pasted image 20251111133425.png]]

- How does $N$ simulate $M$?
- On input $x = a_1a_2...a_n$, $N$ starts with 
	- $⊢ a_1 a_2 a_3 · · · a_n ⊔ ⊔ ⊔ · · ·$
- $N$ copies input in top track, fills other tracks with blanks, shifts everything right one cell and marks left end-markers to denote current head position at starting configuration of $M$ 
	![[Pasted image 20251111133830.png]]

- Each step of $M$ is simulated in several steps of $N$ 
- $N$ at left of tape, scans until sees three marked symbols and determines what to do according to $M$'s $\delta$.
-  These transitions are encoded in $N$'s state control.
- $N$ goes back to the marks and rewrites symbols on tracks appropriately.
- $N$ returns to left end of tape and simulate next step of $M$ 
- This idea can be generalised to TMs with any number of tapes 
- Multiple-tape machines have the same expressive power as single tape-machines. 


#### Universal Turing Machine 
- We have seen that there are TMs that can simulate others TMs.
- We introduce here the concept of a universal TM, i.e. a machine that can simulate all other TMs 
- The idea is to find a suitable encoding of TMs and construct a TM $U$ such that:
	- $L(U) = \{M$#$x | x \in L(M)\}$
- Here "$M$#$x$" means: encoding of $M$ followed by a separator # followed by encoding of string $x$ in $M$'s input alphabet.
- $U$ will work roughly as follows:
	- Check whether $M$ and $x$ are correct encodings, reject if not 
	- Simulate $M$ on $x$ 
	- Accept if $M$ accepts, reject if $M$ rejects.

#### The UTM and Real Life
- The UTM is a complex exercise in hacking TMs 
- Not just a theoretical curiosity, we use things like UTMs every day
- In terms of programming languages, it is an interpreter - a program that takes in a program and input and simulates the expected computation, e.g:
	- a C interpreter written in C
	- a Java interpreter written in Java
	- a Java interpreter written in C, etc.

#### Encoding Turing Machines
- How do we encode TMs?
- Many ways
- Example:
	- First we fix reasonable encoding scheme over alphabet $\{0, 1\}$
- Encoding should be simple enough that all data for a TM can be easily determined by another machine
- Example of encoding (beginning of string)
	- $0^n10^m10^k10^s10^t10^r10^u10^v1$
- Decodes to:
	- States $\{0, 1, ..., n-1\}$,
	- Tape alphabet $\{0, 1, ..., m-1\}$ of which first $k$ numbers is the input alphabet
	- The start, accept and reject states are $s, t$ and $r$.
	- The blank symbol is $u$ and the endmarker is $v$

- The remainder of string can consist of sequence and substrings that specify transitions in $\delta$
- For example: 
	- $0^p10^q10^b10$
- Indicates that $\delta$ contains transition
	- $\delta (p, a) = (q, b, L)$
- And direction to move head is encoded in last digit
- Details of the encoding are not important 
- What's important is that it should be easy to interpret and encode Turing machines.

#### Constructing a UTM $U$
- Once we have a suitable encoding, we construct a universal TM $U$ such that:
	- $L(U) = \{M$#$x|x \in L(M)\}$
- How does $U$ work?
- Given $M$#$x$, $U$ first checks that encodings are correct, if not, it immediately rejects. 
- If encodings are valid, $U$ does step-by-step simulation of $M$.
- Tape is partitioned in three tracks.
	- Top track: description of $M$;
	- Middle track: contents of $M$'s tape;
	- Bottom track: $M$'s current state & position on its tape;
- In each step, $U$:
	- Looks at $M$'s current state and head position (track 3);
	- Reads the tape contents at the correct position (track 2);
	- Reads the relevant transition (track 1);
	- Simulates transition, updating tape, state and head position;
	- Accepts if $M$ accepts, rejects if $M$ rejects.

#### UTM and the Halting Problem
- The UTM we described is very basic, it blindly simulates other TMs.
- It reads (an encoding of) a TM $M$, (an encoding of) an input $x$ and simulates $M$ on $x$:
	- It halts and accepts if $M$ halts and accepts $x$ 
	- It halts and rejects if $M$ halts and rejects $x$ 
	- It halts if $M$ loops on $x$ 
- Can we find a total universal TM that can see if M halts or loops on $x$ (no we can't)


# References