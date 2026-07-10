13-11-2024 15:02

Status:

Tags: [[Mathematics I]]


# Logic

#### Propositions or statements:
- Consider the following arguments:
	- If it is a holiday or I am sick, then I will not go to work. Therefore, if I go to work, it is not a holiday and I am not sick. 
	- For x∈ℤ if x < -5 or x > 5, then |x| > 5. Therefore, if |x| ≯  5, x ≮  -5 and x ≯  5. • 
- They say different things 
- However, their logical form is the same 
	- If p or q then r. Therefore, if not r, then not p and not q. 
- and they are both valid.

#### Arguments and form:
- Syntax 
- Semantics 
- Inference - formal proofs 
	- Deduction: from premises to conclusions
	- Induction: from specific premises to global conclusions

#### Systems of logic:
• Propositional logic 
• First-order logic (predicate logic) 
• Second-order logic 
• Higher-order logic 

• Contextual logics: modal, epistemic, deontic, … 
• Fuzzy logic • Intuitionistic logic 
• …


### Syntax:

#### Propositional variables:
• Consider the previous example. 
	• Propositions or statements 
	• it is a holiday, I am sick, I will not go to work. 
	• x < -5, x > 5, |x| > 5. 
	• Can be true or false but not both 
• Propositional variables 
	• p, q, r 
• Not all assertions are propositions. 
• Not all sentences are assertions.

#### Formulas:
- Some people say formulae
- Syntactic symbols of the language:
	- propositional variable symbols p, q, r
	- unary operation symbol $\neg$ called negation
	- binary operation symbols $\land, \lor, \rightarrow$ called conjunction, disjunction and implication
	- constant symbol $\bot$ called falsity, or contradiction
	- brackets ( , )
- Formulas are built up from the above
	- Should all possible strings with the symbols above be taken as formulas?
	- When is a string that uses the symbols above a formula?

#### Backus Naur Form (BNF):
- V ::= p | q | r | s | ... (propositional variables)
- F ::= V | $\bot$ | $\neg F$ | $F \land F$ | $F \lor F$ | $F \rightarrow F$ | $(F)$ 
- BNF is standard in computer science for defining the grammar of the language (here the language of formulas)
- a formula is a representation of a unique derivation in the BNF
- We will use $\varphi, \psi$ to range over well-bracketed terms built up from the grammar (formulas)

#### Trees:
• A tree is a mathematical structure that has nodes and edges. 
• there is a special node called the root 
• each node has zero or more children 
	• nodes without children are called leaves 
• each node that is not the root has exactly one parent 
• there are no cycles

#### Syntax Trees:

![[Pasted image 20241113152356.png | 600]]

#### Trees, BNF Derivations and terms:
- The following are equivalent things for a grammar:
	- a well-formed well-bracketed term
	- derivation in BNF
	- a syntax tree
- For propositional logic, this means that there are bijections between the [[Sets]] of
	- well-formed well-bracketed formulas
	- derivations in the BNF
	- syntax trees

#### Syntactic Conventions and brackets:
- To write down a derived formula you need brackets to avoid ambiguity
- To reduce the number of brackets there are several conventions:
- $\neg$ binds tighter than $\land$ and $\lor$
- $\land$ and $\lor$ bind tighter than $\rightarrow$ 
- $\land$ and $\lor$ have the same precedence and associate to the left
- $\rightarrow$ associates to the right
# References