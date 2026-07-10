2026-04-20 20:56

Status:

Tags: [[Formal Specification and Verification]]


# Hoare Logic - Sequential and Conditionals

#### Proving the Validity of A statement 
- A statement S is valid if can be derived with inference rules 
- to construct a proof tree where S is the root 
- and leaves and closed by axioms
- We assume that we can prove any logical statements

- A procedure:
	- Start with S as the root 
	- Choosing a rule that simplifies (i.e. breaks down) S leading to zero (closing the proof) or more sub-goals
	- If there are no sub-tree, the proof (for that sub-goal) is done
	- otherwise, repeat the procedure on the sub-trees until all nodes are valid

#### Rule of Composition 
- ![[Pasted image 20260420210529.png]]
- R is an intermediate assertion
- ![[Pasted image 20260420210620.png]]
- More general form:
- ![[Pasted image 20260420210729.png]]
- $R_1, R_2, ... R_{n-1}$  are intermediate assertions 

#### Rule of Conditional 
- ![[Pasted image 20260420211921.png]]
- ![[Pasted image 20260420212026.png]]
- ![[Pasted image 20260420212038.png]]
#### Hoare Logic Rules (so far) 
- ![[Pasted image 20260420212115.png]]
- 
# References