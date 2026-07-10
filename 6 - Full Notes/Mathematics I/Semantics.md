13-11-2024 15:50

Status:

Tags: [[Mathematics I]] [[6 - Full Notes/Mathematics I/Logic]]


# Semantics

#### What is the semantics (meaning) of a formula?
- a propositional variable can either be T(rue) or F(alse)
- a formula $\varphi$ will be T or F depending on the meaning of its sub-formulas
	- i.e. the value of each point in the syntax tree depends on the value of its children (function!)
	- truth tables are a convenient way of expressing this

![[Pasted image 20241113155400.png]]

#### Semantics as a function:
- Let $2=\{F, T\}$ 
- Let $\neg : 2  \rightarrow 2, \lor : 2 \times 2 \rightarrow 2, \rightarrow \,\, : 2 \times 2 \rightarrow 2$ be the obvious functions (note: we are abusing notation)
- suppose that $\lor$ is the set of propositional variables and there is some assignment of truth values $\sigma : V \rightarrow 2$ 
- We will define a function $⟦-⟧σ:F \rightarrow 2$ that takes a formula to its truth value, based on the truth assignments of propositional variables given by $\sigma$ 

#### Semantics as a (recursively defined) function:
- $⟦\bot⟧σ = F$
- $⟦p⟧σ = \sigma (p)$ :
- $⟦\varphi \lor \psi ⟧σ = \lor (⟦\varphi⟧σ, ⟦\psi⟧σ)$ 
- $⟦\varphi \land \psi ⟧σ = \land (⟦\varphi⟧σ, ⟦\psi⟧σ)$ 
- $⟦\varphi \rightarrow \psi ⟧σ = \rightarrow (⟦\varphi⟧σ, ⟦\psi⟧σ)$ 
- $⟦\neg \varphi⟧σ = \neg (⟦\varphi⟧σ)$ 
- Notice that the function depends on the particular assignment $\sigma$ 

#### Tautologies:
- a formula $\varphi$ that evaluates to T for all possible values of propositional variables is called a tautology, or is said to be valid
- a formula $\varphi$ that evaluates to T for at least one assignment of truth values to propositional variables is said to satisfiable
- two formulas are logically equivalent when they evaluate to equal truth values for any assignment of truth values to propositional variables
	- note: logical equivalence is an equivalence relation on the set of all formulas!

#### Semantic Entailment:
- Recall that a tautology is formula $\varphi$ that evaluates to T for all truth assignments to propositional variables:
	- write $\models \varphi$
	- the symbol $\models$ is called "semantic entailment"
- Suppose that $\Gamma$ is a set of formulas
	- $\Gamma \models \varphi$ (read $\Gamma$ semantically entails $\varphi$) means: any truth assignment that makes all the formulas of $\Gamma$ evaluate to T also makes $\varphi$ evaluate to T
	- so $\models \varphi$ is simply shorthand for $\emptyset \models \varphi$ 
- is $\Gamma \models \varphi$ a syntactic property or a semantic property of $\varphi$

#### Formal Proof Systems:
- Suppose that we some formal proof system
	- a collection of rules that allows us to form formal things called proofs - taking some formulas as assumptions and producing a conclusion
	- natural deduction (Gentzen) is an example of formal proof system (next lecture), but there are several other proof systems
- Write $\Gamma \vdash \varphi$ when, taking the formulas in $\Gamma$ as assumptions we can prove $\varphi$ as the conclusion
- Write $\vdash \varphi$ when we can prove $\varphi$ without using any assumptions (i.e. as shorthand for $\emptyset \vdash \varphi$ )

#### Soundness:
- When is a proof system correct?
- $\Gamma \vdash \varphi$ implies $\Gamma \models \varphi$ 
- "whenever gamma proves phi, gamma semantically entails phi"
- So if we can prove that $\phi$ holds given from some assumptions, if those assumptions are true then $\phi$ must be true also!
- i.e. if we can prove something in our proof system then it is true 

#### Completeness:
- When is a proof most useful?
- $\Gamma \models \varphi$ implies $\Gamma \vdash \varphi$ 
- "whenever gamma semantically entails phi, gamma proves phi"
- whenever $\phi$ is given that some formulas are true, then $\phi$ is also provable from those formulas
- i.e. if something is true, the proof system is powerful enough to prove it 
# References