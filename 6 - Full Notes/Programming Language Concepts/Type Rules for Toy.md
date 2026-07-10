2026-04-09 15:54

Status:

Tags: [[Programming Language Concepts]]


# Type Rules for Toy

#### Values 
- It is useful to name the rules (cf. TNat, Tt, Tf).
	![[Pasted image 20260409155504.png]]

#### Conditionals 
- Rule for if:
	![[Pasted image 20260409155542.png]]

#### Typing Let
- Consider the local variable construct.
	![[Pasted image 20260409155603.png]]
- A first guess would be 
	![[Pasted image 20260409155941.png]]
- But this is wrong 

#### Free Variables 
- Consider:
	![[Pasted image 20260409155832.png]]
- Use the incorrect rule:
	![[Pasted image 20260409155847.png]]
- How can you fill the hole without knowing anything about $x$?

#### Contexts 
- In order to type $e$, we need to keep the types of its free variables. We keep these assumptions in contexts, usually denoted by capital Greek letters e.g. $\Gamma, \Delta, ...$ 
- Formally, a context is a mapping from variable names to Types. We write contexts as comma-separated lists
	- e.g. $Γ = x : N, y : B, z : N,…$

#### A Correct Rule for Let
- Our type relation $⊢ e : τ$ needs to include the context. 
- We write $\Gamma \, ⊢ e : τ$ to mean that in context $\Gamma$, $e$ has type $\tau$.
	![[Pasted image 20260409160624.png]]

#### Variables
- Rule for variables:
	![[Pasted image 20260409160655.png]]

#### Comparison
- Rule for comparison:
	![[Pasted image 20260409160715.png]]

#### Addition
- Rule for addition:
	![[Pasted image 20260409160737.png]]

#### Full Type System
![[Pasted image 20260409160753.png]]

# References