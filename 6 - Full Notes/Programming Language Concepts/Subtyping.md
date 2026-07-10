2026-04-13 10:52

Status:

Tags: [[Programming Language Concepts]]


# Subtyping

#### Example
- Consider an expression language with record types:
	![[Pasted image 20260413105325.png]]
- The function expects the argument $\{x : ℕ\}$, but we have $\{x : ℕ, y : ℕ\}$ 
- Is this program well typed?

- According to our typing rules - no:![[Pasted image 20260413105502.png]]

#### Over-specification
- Sometimes type systems force us to be too specific. 
	- E.g. example on previous slide:
		- f needs any record that at least contains $x : N$
	- Another example:
		- Length of an array does not need to know the type of its elements
- We are looking for a generic (or polymorphic) type for the function arguments 
- Many mainstream programming languages support generics or polymorphism in terms of both specification and implementation.

#### Polymorphism 
- Polymorphic means "many shaped" 
- A polymorphic function admits arguments of different types 
- Kinds of polymorphism:
	- Parametric polymorphism (C++ Templates, Java Generics)
	- Subtype polymorphism (OO: C++, Java, etc)  
	- Ad hoc polymorphism (overloading of functions and methods)
- We focus on subtype polymorphism

#### Types-As-Sets Subtyping 
- Given an interpretation $[\_]$  of types as sets, we can say that $τ <: σ$ when: 
	- $[τ] ⊆ [σ]$
- General definition, but not syntactic

#### Structural Subtyping 
- Define $τ <: σ$ when every operation that can be performed on $\sigma$ can also be performed on $\tau$.
- This incorporates lots of structural properties, e.g., pairs must be subtypes of pairs because of the projection operations.

#### Nominal Subtyping 
- Explicitly declare what types are subtypes of others and ensure that any operations valid on a supertype are valid on the subtype.
- This is the approach taken in OO, via inheritance

#### Subsumption and the Subtype Relation
- The subsumption property says: if $\tau$ is a subtype of $\sigma$ then every value of $\tau$ can also be considered as a value of $\sigma$.
	![[Pasted image 20260413111319.png]]
- The rule applies to both nominal and structural subtyping, but it relies on the $τ <: σ$ relation

#### Nominal Subtyping
- types are distinguished by their names, hence the following types are different:
	![[Pasted image 20260413112002.png]]
- $f: A\rightarrow X$ cannot be applied to $e: B$.

- Type names hide the underlying structure, allowing programmers to enforce the distinction at the type level. E.g.
	![[Pasted image 20260413112104.png]]

#### Subtyping Relation
- Explicitly specify the relationships between the named types using some syntax:
	![[Pasted image 20260413112205.png]]
	![[Pasted image 20260413112217.png]]

#### Structural Properties 
- Declaring arbitrary types as subtypes may break subsumption. For example, what does it mean if $N × N <: N × N × N$?
	- Java overcomes this by only allowing subtyping between classes 
	- Inheritance forces that every member in the supertype also exists in the subtype.







# References