2026-04-17 12:31

Status:

Tags: [[Programming Language Concepts]]


# Operational Semantics

#### Definition 
- An alternative approach to semantics is to build an inductive binary relation between the terms of the language
- There are two types of operational semantics: big step and small step
- In big step semantics the binary relation is between terms and values. it represents the values that a term can evaluate to.
- We typically write $E ⇓ V$ to mean program E evaluates to value V
	- The meaning of the program is given by the values it can evaluate to value V 
	-  Modelling the run time environment (e.g. a heap) is quite straightforward in this approach by defining the relation between run time states and values.
	- The program operators are often easily specified in terms of "what they do" rather than "what they mean" 
- One disadvantage of this approach is that it still doesn't account for the effects of non-terminating programs very easily. 

#### Big Step Toy Semantics 
 - Let's give an inductive relation for the big-step semantics for the Toy language:
 - The form of the relation will be $E ⇓ V$ 
	 ![[Pasted image 20260417124231.png]]

	![[Pasted image 20260417124608.png]]
- Big Step semantics still don't model the sequence of computation steps a program can take though - this can be problematic when modelling, e.g. concurrency. 

#### Small step operational semantics 
- In contrast, small step operational semantics are given by an inductive relation between terms representing run time states of programs.
- Run time state include the heap, stack and program counter etc.
- We typically represent changing program counters as changing terms of a language. For example we write $E \rightarrow E'$ for our reduction relation.
- This means, program state E evaluates in "one" step of evaluation to program state E'.
- By considering the evaluation of a program step-by-step then we can can see clearly how a program behaves. 
- To determine whether a program calculates a given return value then we repeatedly follow a the single steps of evaluation until a value is reached.
- Non-termination is an activity (infinite set of steps) rather than failure to calculate a value.
	- Useful for analysing at what point programs begin to diverge and what effects they may have during divergence.

#### Small Step Toy Semantics
- The form of this relation is $E \rightarrow E'$ this represents a single step of computation of program state E reach the runtime state E' (which can be represented as another expression).
	![[Pasted image 20260417125238.png]]
	![[Pasted image 20260417125507.png]]

#### Example of a Big Step Proof Tree
- The example is:
	![[Pasted image 20260417125611.png]]
- The inductive rules in the big step semantics form a proof tree to justify the final conclusion
	![[Pasted image 20260417125659.png]]
#### Example of a Small Step Proof Tree
- Same program.
	![[Pasted image 20260417125840.png]]

#### Small Step Proof Trees
- For our example, small step semantics requires five evaluation steps to reach the value 53. Each single step is given by a proof tree that justifies it.
- We sometimes write this sequence of steps without showing the proof trees.
	![[Pasted image 20260417141721.png]]

#### Relating Small Step and Big Step Semantics 
- Ideally, if we have defined our semantics correctly , then we should have a strong relationship between the big step and small step semantics.
- They should specify the same behaviours - in different ways
- Iff there exists a (possibly empty) sequence
	![[Pasted image 20260417142050.png]]
- We can prove the following Theorem for the Toy language semantics
	![[Pasted image 20260417142108.png]]





# References