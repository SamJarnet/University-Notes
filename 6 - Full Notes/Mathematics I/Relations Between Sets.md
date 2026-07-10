28-10-2024 22:14

Status:

Tags: [[Mathematics I]] [[Sets]] 

# Relations Between Sets

#### Examples of relations:
- When X=Y, instead of saying that R is a relation from X to X we usually say that R is a relation on X. 
- Examples:
	- The full relation X x Y, the empty relation $\emptyset \subseteq X \times Y$
	- There is a relation on any set X called the identity relation $I_X = \{(x,x) | x \in X\}$

![[Pasted image 20241102152927.png|]]

#### Composition of relations:
- if R is a relation from X to Y and S is a relation from Y to Z then R ; S is a relation from X to Z defined:
	- $(x, y) \in R ; S$ if there exists $y \in Y$ such that $(x,y) \in R$ and $(y,z \in S)$
	- R ; S is sometimes written as $S \circ R$
	- Composition is associative

#### [[Functions Between Sets]] are special relations:
- Any function $f: X \rightarrow Y$ is a special kind of relation from X to Y that satisfies:
	- for all $x \in X$ there exists a unique $y \in Y$ s. t. $(x,y) \in f$
	- if $(x, y) \in f$ and $(x, z) \in f$ then $y=z$ 
- Given a function f, when we want to emphasize that we are talking about a relation, we call it the graph of f



# References