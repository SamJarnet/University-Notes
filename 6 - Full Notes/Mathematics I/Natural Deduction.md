15-11-2024 23:14

Status:

Tags: [[Mathematics I]] [[6 - Full Notes/Mathematics I/Logic]]


# Natural Deduction


#### Formal Proofs:
- Recall: syntax trees:
	- internal node labelled with operations ($\neg, \land, \lor, \rightarrow$)
	- leaves labelled with propositional variables (p, q, r, ...) or constant ($\bot$) 
- Formal proofs in natural deduction (aka derivations or proof trees) are different kinds of trees
	- nodes labelled with formulas
	- labels of each parent & its children correspond to particular proof rule
	- leaves are assumptions traditionally drawn with leaves (assumptions) at the top and the root (conclusion) at the bottom

#### Proofs in Natural Deduction:
- A proof can be seen as tree where
	- leaves are assumptions
	- the root is the proved formula
	- the internal nodes are determined by applications of proof rules
- In natural deduction, proof rules naturally fall into two classes
	- introduction rules - allow the introduction of a logical connective
	- elimination rules - allow the elimination of a logical connective 

![[Pasted image 20241115232407.png|400]]

### Rules of Natural Deduction:

#### Rules for conjunction:

![[Pasted image 20241115232502.png]]

- one introduction rule, two elimination rules

#### Rules for implication:

![[Pasted image 20241115232704.png]]

- one introduction rule, one elimination rule 

![[Pasted image 20241115232952.png]]

#### Discharging Assumptions:

![[Pasted image 20241115233041.png]]

#### Rules for negation:

![[Pasted image 20241116170254.png]]

#### Rules for disjunction:

![[Pasted image 20241116170338.png]]

- two introduction rules, one elimination rule

#### Rules for "False":

![[Pasted image 20241116170452.png]]

- Note: the second rule is non-constructive: intuitionistic logic rules it out

![[Pasted image 20241116170557.png]]

#### Classic vs Intuitionistic:
![[Pasted image 20241116170722.png]]

- The two rules have the same power
- Using these rules can result in proofs where you prove that something exists, but don't know what it is

Example:
- Theorem. There exist irrational numbers $p, q$ such that $p^q$ is rational
- Proof. Consider $\sqrt{2}$ and $(\sqrt{2})^{\sqrt{2}}$. It is well-known that $\sqrt{2}$ is not rational
- Now either $(\sqrt{2})^{\sqrt{2}}$ is rational or it is not (excluded middle!). If it is rational then we are finished: let $p=q=\sqrt{2}$. If not, let $p =(\sqrt{2})^{\sqrt{2}}$ and $q=\sqrt{2}$. Then $p^q$ is rational since $(\sqrt{2}^{\sqrt{2}})^{\sqrt{2}} = (\sqrt{2})^{\sqrt{2} \times \sqrt{2}} = (\sqrt{2})^2 = 2$ 
- So we proved what we wanted but we still don't know what p is! 
#### Proving Soundness:
- Proof (sketch): Induction on the length of the natural deduction proof
	- e.g. V-elimination
	![[Pasted image 20241116171915.png]]

- assume that an assignment of truth values makes $\varphi \lor \psi$  true
- then one of $\varphi$ or $\psi$ is true
- in each case, use inductive hypothesis to get X true

#### Completeness: 
- Completeness of a set of proof rules means that there are "enough proof rules to prove all theorems, i.e. all true statements"
- Completeness Theorem: $\Gamma \models \varphi$ implies $\Gamma \vdash \varphi$

# References
