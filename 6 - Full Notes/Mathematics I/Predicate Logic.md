16-11-2024 17:25

Status:

Tags: [[Mathematics I]] [[6 - Full Notes/Mathematics I/Logic]] [[Semantics]]


# Predicate Logic

#### Propositional Logic vs Predicate Logic
- In propositional logic, a "world" is an assignment of truth values to propositional variables
- Predicate logic (also called first order logic) is a much richer language
	- a world is set, together with relations (predicates) and functions. Given a set A:
		- a n-ary function is a function of type $A^n \rightarrow A$
		- a n-ary relation is a subset of $A^n$ 

#### E.g. Predicate Logic Formula:
- Recall the definition of injective function. A function $A \rightarrow A$ is injective when "for all x and y in A, if f(x) = f(y) then x=y"
- The above can be translated into a formula of predicate logic
	- $\forall x.\, \forall y. (f(x) = f(y)) \rightarrow (x=y)$
- Then a world will satisfy (model) the formula exactly when f is an injective function in that world

#### BNF for predicate Logic:
- variables (V), constants (C), function symbols, relation symbols
- Terms:
![[Pasted image 20241116173437.png]]

#### Semantics of Predicate Logic:
- Model:
	- a set A called the domain
		- for each constant symbol a, an element $a \in A$
		- for each n-ary function symbol f, a function $f:A^n \rightarrow A$
		- for each n-ary relation symbol R, a subset $R \subseteq A^n$ 
			
			![[Pasted image 20241116173758.png|300]]
- Given a function $\sigma$ from variable to elements of A, any term now has a corresponding element of A
#### Semantics of Terms:
$T ::= V | C | f(T, T, ..., T )$
- $⟦x⟧σ = σ(x)$
- $⟦a⟧σ = a$ 
- $⟦f(t_1,t_2,...,t_k)⟧ σ = f(⟦t_1⟧σ,⟦t_2⟧σ,...,⟦t_k⟧σ)$

#### Semantics of Formulas (Tarski):
- if $\phi = R(t_1, t_2, ..., t_k)$ then $A \models_{\sigma}\phi$ iff $(⟦t1⟧σ,⟦t2⟧σ,...,⟦tk⟧σ)∈R$
- if $\phi = \neg \psi$ then $A_1 \models_{\sigma} \phi$ iff $A \models_{\sigma} \psi$ does not hold
- if $\phi = \psi_1 \lor \psi_2$ then $A \models_{\sigma} \phi$ iff $A \models_{\sigma} \psi_1$ and $A \models_{\sigma} \psi_2$ 
- ...
- if $\phi = \exists x.\psi$ then $A \models_{\sigma} \phi$ iff there exists $a \in A$ such that $A \models_{\sigma} [x⟼a] \psi$
- if $\phi = \forall x.\psi$ then $A \models_{\sigma} \phi$ iff for all $a \in A$ we have $A \models_{\sigma} [x⟼a] \psi$  
- If $A \models_{\sigma} \phi$ then we say A is a model for $\phi$ 

#### Logical Equivalence
- Two formulas $\phi, \psi$ are logically equivalent ($\equiv$) if for any model we have $A \models \phi$ iff $A \models \psi$ (logical equivalence is an equivalence relation)
![[Pasted image 20241116183737.png]]

- note: x does not appear in $\psi$ 

#### Semantic Entailment:
- Propositional logic:
	- $\Gamma \models \varphi$ means: any truth assignment that makes all the formulas of $\Gamma$ evaluate to T also makes $\varphi$ evaluate to T
- Predicate logic:
	- $\Gamma \models \varphi$ means: any model A for all the formulas of $\Gamma$ is also a model for $\varphi$ 

#### Natural Deduction for Predicate Logic:
![[Pasted image 20241116184325.png]]

#### Example Proof:
![[Pasted image 20241116184450.png]]

#### Soundness and Completeness:
- As for predicate logic, natural deduction with the additional rules sound and complete
- $\Gamma \models \varphi$: any model A for all the formulas of $\Gamma$ is also a model for $\varphi$ 
- Soundness: $\Gamma \vdash \varphi$ implies $\Gamma \models \varphi$
- Completeness: $\Gamma \models \varphi$ implies $\Gamma \vdash \varphi$  
- 
#### Gödel’s Incompleteness Theorem
- We have discussed two sound and complete proof system
- Sometimes it is impossible to get a sound and complete system, for example, there is no finite set of rules that are sound and complete for all the true statements about the natural numbers!
	- Gödel’s incompleteness theorem 
	- in fact, the situation is even worse, it is actually impossible to write a computer program that lists an infinite set of rules that would all together be complete 
- So mathematicians are useful after all!





# References