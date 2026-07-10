2026-04-11 17:13

Status:

Tags: [[Programming Language Concepts]]


# Structured Types

#### The Shape of Data
- Programs manipulate data which comes in different shapes.
- Structured types help us encode data of different shapes, e.g. pair of integers, a 3-element list of integers, a binary tree with integer nodes, etc.

#### The Unit Type
- The type that has exactly one value. We call the type Unit and its value is ()
	![[Pasted image 20260411171520.png]]
- In Haskell the type is (), the value is ().
- Argument type of a no parameter C/Java function:
	- int foo() {...}.
- Void return type in C/Java
- Can be used to suspend the evaluation:
	![[Pasted image 20260411171626.png]]

#### Pairs
- Given two pieces of data of types $\tau$ and $\sigma$, we can form a piece of data of type $\tau \times \sigma$. Constructor for this type is a pairing operation, usually written as (t, s). 
	![[Pasted image 20260411171848.png]]
#### Tuples
- Generalise pairs to arbitrary tuples by allowing the constructor to accept arbitrary number of elements.
	![[Pasted image 20260411171940.png]]
- Pairs and tuples are very common structured types.

#### Pair/Tuple Destructors
- We referred to ( _ , _ ) as constructor.
- The dual operations are called destructors:
	![[Pasted image 20260411172100.png]]
- In languages with pattern matching we can write:
	- match e with (e1, e2) -> ...
- For tuples we need $n$ destructors.

#### Records 
- Consider tuples as collections of $n$ elements indexed by integers. Introduce labels to index the elements. This corresponds to struct in C and objects in Java.
- Type: {l1:t1, l2:t2, ..., ln:tn} where l$i$ are labels (fields) and t$i$ are element types
- Constructor:
	- common syntax: {$l_1 = e_1, ..., l_n=e_n$}
		![[Pasted image 20260411172401.png]]
- Destructors:
	- Common syntax _ . _
		![[Pasted image 20260411172442.png]]

#### Lists
- Ordered finite sequences of elements
- Given the element type $\tau$ we can form List $\tau$ with constructors $[]$ and _ : : _ 
	![[Pasted image 20260411172603.png]]
- In Haskell the type is $[\tau]$ and constructors are $[]$ and _ :  _
- Destructors:
	![[Pasted image 20260411172657.png]]
- These destructors are not type safe as does not check for empty lists which could cause errors. Languages solve this with Maybes or with pattern matching to handle it.

#### Sum Types
- A pair $\tau \times \sigma$ keeps the data of both $\tau$ and $\sigma$. The sum type keeps the data of either $\tau$ or $\sigma$. 
- Written as $\tau + \sigma$.
- Constructors (inl and inr) are called injections, and they are given by the following rules:
	![[Pasted image 20260411173744.png]]
- Destructors:
	![[Pasted image 20260411173807.png]]
	![[Pasted image 20260411173922.png]]
- In languages with pattern matching 
	![[Pasted image 20260411173933.png]]
- Uniqueness of sum types:
	- Consider the type of inl 3
	- It could be $N + N, N + B$, and infinitely many other types. This breaks inversion lemma, making type checking more complicated. Possible solutions:
		- Introduce type variables into type checking 
		- Require programmers to annotate types
		- Use unique labels instead of inl and inr for every sum type

#### Variant Types
- Generalised sum types that allow more than two members. The type is $⟨l_1 : τ_1,…l_n : τ_n⟩.$
- Constructors are labels injections: $<$l1 = e$>$
- Destructor is a generalised case-expression.
	![[Pasted image 20260411174330.png]]
- Uniqueness of variant types:
	- Consider types $τ = ⟨L : N, R : B⟩$ and $σ = ⟨L : N, X : B⟩$. What type is L 5?
	- Haskell will complain about the types
		![[Pasted image 20260411174449.png]]

#### Enumerations 
-  A variant type where only labels matter, e.g. a type for days of the week
- We can model this type with variants as <Mon: Unit, Tue: Unit, ...> with values <Mon = ()>, …
- Enumeration is a syntactic sugar for these cases. In Haskell
	![[Pasted image 20260411180547.png]]:

#### Option Types
- An important idiom involving variants is optional values of some type $\tau$: <Nothing: Unit, Just: τ> . In Haskell:
	![[Pasted image 20260411180655.png]]

#### A Type Rule For Match?
- Suppose that we want to introduce pattern matching in Toy (similarly to case_of_ in Haskell) - a general destructor for structured types.
- Syntax would look like:
	![[Pasted image 20260411180811.png]]
- where p$i$ are patterns (e.g. inl x, (x, y)).
- Type rule sketch:
	![[Pasted image 20260411180842.png]]
- Where ctx($p_i$) are assumptions about bound variables in patterns (e.g. ctx(inl $x$) = $x : \tau$, ctx(($x, y$)) = $x : \tau, y : \sigma$). This requires a new language for patterns.
# References