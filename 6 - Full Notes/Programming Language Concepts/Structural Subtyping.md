2026-04-13 11:41

Status:

Tags: [[Subtyping]] [[Programming Language Concepts]]


# Structural Subtyping

#### Structural Subtyping 
- Relies purely on the structure of the type to define the subtyping relation. 
- First, the relationship between base, or primitive types, needs to be specified, e.g. 
	- short <: int, float <: double
- Then structure determines the rest.

#### Pair Subtyping
- For example, a subtype of the pair type $\tau \times \sigma$ is a pair of subtypes of $\tau$ and $\sigma$ separately 
	![[Pasted image 20260413114525.png]]

#### Record Subtyping 
- Record types are a generalisation of pair types, and the subtyping relation on records generalises as well.
- Record types don't rely on syntactic positioning in the values for their indexing. E.g. a record with some fields missing may be a well formed record value (of another type). We can't do the same with a tuple.
- Subtyping rules for records can be built up in stages
- First we generalise what we saw above for pairs
- This is called depth subtyping for records:
	![[Pasted image 20260413114732.png]]
- Then we have the notion of width subtyping in which there may be extra fields in the subtype:
	![[Pasted image 20260413114816.png]]
- And finally, we allow reordering of the listed fields:
	![[Pasted image 20260413114834.png]]
- Not all languages adopt all of these principles. E.g. Java does not allow depth subtyping: methods or fields in a subclass cannot have subtypes of that which they are declared in the supertype. 
- Example:
	![[Pasted image 20260413115057.png]]

#### Variants 
- For sum types $\tau + \sigma$, it is intuitive that any value of type $\tau$ can be considered as also being of type $\tau + \sigma + \delta$ as the value of type $\tau$ is still just injected into the sum, albeit into a larger sum.
- For generalised, variant types we have the same notations of width depth and permutation subtyping as we do for records.
- Rules:
	- There is an inversion in the rule for width subtyping 
		![[Pasted image 20260413134513.png]]
	- We can see that we can inject into a larger variant type.
	- The notions of depth and permutations are similar to records
		![[Pasted image 20260413134709.png]]

#### Covariance and Contravariance 
- Relationship between the subtyping on the types of substructure and the subtyping of the structure itself
#### Covariance 
- For pairs (records) and sums (variants) the ordering between $\tau$ and $\sigma$ is "preserved" in the later subtyping relation
	![[Pasted image 20260413134912.png]]
- This preservation of order is called covariant. Records and variants are both covariant type formers.

#### Contravariance 
- Some type formers do not behave like this. Suppose a type former Foo, e.g. if $\tau$ is a type, Foo $\tau$ is also a type.
- Assuming that:
	![[Pasted image 20260413135030.png]]
 - Foo is a contravariant type former.

#### Function Subtyping 
- Function type former is covariant in its return type and contravariant in its argument type
	![[Pasted image 20260413135129.png]]

#### Lists 
- The List type former is covariant 
	![[Pasted image 20260413135151.png]]

#### Arrays
- An array is non-structural in the sense that we don't build elements of the type using data constructors. Elements in the array can be modified.
- Arrays consume data on update and produce data on selections. These two operations have different variance requirements.
- Array selections force covariance: $τ[] <: σ[]$; I select an element from $a : σ[]$, but actually $a : \tau[]$, then I need $τ <: σ$ to convert the selected element. 
- Array updates force contravariance: $τ[] <: σ[]$; I  update an element of $a : σ[]$ with the new value $x : \sigma$, but then $a$ is actually $\tau[]$, then I need $τ <: σ$ to convert $x$. 
- We say that arrays are an invariant type former with subtyping rule: 
	![[Pasted image 20260413135605.png]]

#### Subtyping Arrays in Java
- Arrays in Java are covariant. While this is appealing, here is a problem
	![[Pasted image 20260413135648.png]]
- passes type-checker, but throws exception at runtime. java is not type safe due to covariant array types.

# References