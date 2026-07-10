 2026-04-08 16:29

Status:

Tags: [[Programming Language Concepts]]


# Type Derivation Rules

#### What is Well-Typed?
- Most typed languages require explicit type annotations e.g.
	- In C variables are annotated with a (weak) which helps the compiler to allocate enough memory for the values of that type. 
	- In Java methods are annotated with the type of their input parameters and return value. 
- The way that the compiler makes use of these annotations determines whether the type system is.

- The remainder of the lecture is strong(static ) typed systems
- Proving well-typedness
	- The compiler needs to check that the program never consumes data of the wrong type while executing.
	- Some operators consume data, so the compiler needs to find/check uses of these operators.
	- Checking well-typedness of programs amounts to checks on abstract syntax trees according to the types of the data being used.

#### A Toy Language
- Grammar for Toy:
	![[Pasted image 20260408165733.png]]
- Where $n$ rangers over natural numbers and $x$ rangers over some set of variable names.
	![[Pasted image 20260408165814.png]]
- Tree:
	![[Pasted image 20260408165823.png]]
- Checks all leaves then all parents of those leaves and continues until complete 
	![[Pasted image 20260408165937.png]]


#### Type Checking 
- One way of checking types is to traverse the AST and see whether the operators that consume data are given data of the correct type.
- The operators that consume data are:
- if_then_else_ (consumes $\mathbb{B}, τ, τ$),    _ <_  and _ +_ consume $(\mathbb{N}, \mathbb{N})$


#### Complicated Example
- E.g.
	![[Pasted image 20260409151919.png]]
- So is this program well typed? In a dynamically typed language you might say so. What about a statically-typed one?
- The sub-tree is neither $\mathbb{N}$ or $\mathbb{B}$ - but which one depends on the conditional, which in general is undecidable.

#### Type Checking Lessons
- Every sub-tree of the AST needs to be given a type T in order to check whether the whole AST is well-typed.
	- We need to define the "typing relation" written 
		- $⊢ e : τ$ (means $e$ has type $τ$)
	- We need to define this for all programs in Toy.
- We will want to do local type-checking on syntax trees.
	- The type of a program $(f \, e_1...e_n)$  should depend only on the types of $e_1...e_n$.
	- Only certain operators generate actual checks for correct usage of types.
	- We may need to approximate the type where it cannot be determined statically.


#### Derivation rules
- The general form of a type derivation rule is:
	![[Pasted image 20260409152638.png]]
- It means "if the relation holds for the thing above the line then the relation holds for the thing  below the line". There might be no premises above the line.
- In general, a programming language will be given a set of such rules. In order to show $⊢ e : τ$, then rules must be formed in to a tree such that leaves have no premises.
	![[Pasted image 20260409152911.png]]

#### Inductive Sets
- Suppose that you want to build an infinite set of strings $S$, that respects the following rules:
	- $a$ and $b$ are in $S$ 
	- If $\alpha \in S$ then $\alpha c$ is in $S$ 
	- If $\alpha \in S$ and $\alpha$ ends with $c$, $\alpha d$ in $S$ 
	- take the smallest such set
- Examples:
	- $a, b, acc, acd, accdccd, ...$ 
- The minimality requirement and the fact that all the constructors are in $S$ mean that any element of $S$ must be one of:
	- $a, b, \alpha c, \alpha c d$   ,       $\alpha \in S$ 
- We can give a grammar to $S$:
	- S ::= a | b | Sc | Scd

#### Using Inductive Sets
- In order to define a function or relation on $S$, it is sufficient to define the function or relation inductively by specifying it on the generating shapes, e.g.
	- f a  = 0
	- f b = 0
	- f (s.c) = f s
	- f (s.c.d) = 1 + f s
- and then asking for the smallest function that satisfies these rules 
- Defining a function or relation on the set of all programs of a programming language P, means defining it on all constructors of P.
- This is handy because we need to define typing relations $⊢ e : τ$ for all programs in the toy language.
- Because the set of all programs is inductively defined by its operators. we can do this one operator at a time.

#### Example Derivation
- Let us define derivation rules for "balanced terms in $S$"
	![[Pasted image 20260409154409.png]]
- A proof that $acdcd$ is balanced 
	![[Pasted image 20260409154456.png]]














# References