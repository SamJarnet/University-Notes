2026-04-10 16:49

Status:

Tags: [[Type Rules for Toy]] [[Programming Language Concepts]]


# Adding Functions For Toy

#### Lambda Calculus 
- Consider adding $\lambda$-calculus like functions to Toy.
- We need function abstraction and application operations.
- In its un-typed form, it is Turing complete - i.e. all computations can be expressed in it.
- This changes if we introduce simple types.

#### Example Lambda Terms
- The identity function: $λx.x$
- First projection: $λx.λy.x$
- Second projection: $λx.λy.y$
- Twice : $λf.λx.f (f \, x)$
- Composition :  $λf.λg.λx.f (g \,  x)$

#### Extending Toy
- We need a type for functions e.g. $\tau \rightarrow \sigma$ is a function that takes data of type $\tau$ and returns data of type $\sigma$.
	![[Pasted image 20260410165547.png]]


#### Typing Rules 
- The type rules for the added constructs are straightforward given what we have learnt already about contexts:
	![[Pasted image 20260410165653.png]]

#### Types In Lambda Calculus 
- $λ(x : τ).x : τ → τ$
- $λ(x : τ).λ(y : σ).x : τ → σ → τ$ 
- $λ(x : τ).λ(y : σ).y : τ → σ → σ$ 
- $λ(f : τ → τ).λ(x : τ).f (f x) : (τ → τ) → τ → τ$
- $λ(f : σ → δ).λ(g : τ → σ).λ(x : τ).f (g x) : (σ → δ) → (τ → σ) → τ → δ$

#### Full Type System 
![[Pasted image 20260410171436.png]]

#### The Identity 
![[Pasted image 20260410172123.png]]

#### First Projection
![[Pasted image 20260410172142.png]]

#### Second Projection 
![[Pasted image 20260410172204.png]]

#### Twice
![[Pasted image 20260410173019.png]]

#### Composition
![[Pasted image 20260410173033.png]]



# References