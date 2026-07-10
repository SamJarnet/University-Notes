2026-04-10 17:31

Status:

Tags: [[Type Rules for Toy]]  [[Programming Language Concepts]]


# Implementing Typing Rules

#### Approach
- Recall that the typing relation $\Gamma ⊢ e : τ$ is defined as the smallest relation which satisfies the set of rules 
	- Logically then, if a given program $e$ is in this relation with type $\tau$ then the only way it got into the relation was by using one of the rules.
	- But which one?

#### Syntax Directed Rules 
- A set of inference rules $S$ that defines an inductive relation $R$ is called syntax-directed if for any program $e$ in $R$ there exists exactly one rule in $S$ with such conclusion 
	![[Pasted image 20260410175656.png]]

#### Derivation Structure 
![[Pasted image 20260410175718.png]]  
![[Pasted image 20260411161525.png]]

#### Inversion Lemma
- An important property of a typing relation is called Inversion.
- This is the ability to infer the types of subprograms from the types of the whole program - essentially by reading the type rules from bottom to top.

#### Inversion For Toy
- ![[Pasted image 20260411162950.png]]
- ![[Pasted image 20260411163135.png]]
- Easy to prove - yields a direct algorithm for working out types.

#### Type Checking Algorithm
- ![[Pasted image 20260411163438.png]]

#### Implicit Type Annotations 
- In Toy, we declare the type of bound variables explicitly:
	- $λ(x : τ).e$ let $(x : τ) = e_1$ in $e_2$
- Common practice in C, C++, Java
- One of the points that advocates for dynamically typed languages use to criticise static typing - a burden to the programmer

- What about a statically-typed language without explicitly typed declarations for variables, functions, etc?
- The type checker would need to infer these types from their usage in the code.
- E.g. Let x = 20 in y + x, would reasonably allow the type checker to deduce that x and y must be int
- This is common in many functional languages like Haskell.

#### Type Inference 
- For languages with implicit types, we often refer to the type checking part of compilation as Type inference rather than type checking.
- Type inference is more algorithmically complicated than Type Checking

#### Inference vs Checking 
- Consider Toy rule for Lambda:
	![[Pasted image 20260411164346.png]]
- Get rid of the annotation, write $\lambda x.e$. The new rule:
	![[Pasted image 20260411164420.png]]

#### Type Variables
- The usual solution is to introduce Type Variables .
- I.e. symbolic values that represent an unknown or unconstrained type.
- When typing an expression with unknown types, type variables are used and type checking continues.
- As part of type checking, certain constraints on type variables will arise. E.g. $e$ of unknown type $\tau$ is used if e then ... , meaning that $\tau = \mathbb{B}$.

#### Unification
- The type checking algorithm produces types that may contain type variables and constraints on them.
- To obtain an actual type for the program we need to solve the constraints. I.e. find the substitution of type variables such that all of the constraints hold.
- This latter process is called unification 
- This is the basis of type inference in Haskell - their type variables are represented as types written as e.g. $a, b$ and $c$.

#### Unification Example
- ![[Pasted image 20260411165307.png]]
- t : a, let u = ... : b
- $\lambda$x... : a  $\Rightarrow$ x : c, if (x<3)... : d, $K = \{a = c \rightarrow d\}$.

# References