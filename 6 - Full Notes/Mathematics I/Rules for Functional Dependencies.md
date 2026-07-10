29-10-2024 13:18

Status:

Tags: [[Data Management]] [[Structured Data]] [[Database Systems]]


# Rules for Functional Dependencies


## "Armstrong's Axioms:"

#### Splitting/Combining rule 
- $A_1,…,A_n \rightarrow B_1, B_2, …, B_m$ iff
	- $A_1,…,A_n \rightarrow B_1$
	- $A_1,…,A_n \rightarrow B_2$
	- $A_1,…,A_n \rightarrow B_m$
- e.g. title, year $\rightarrow$ genre, studioName

#### Trivial dependencies:
- for a set B ⊆ {$A_1, ..., A_n$} then trivially: $A_1, ..., A_n \rightarrow B$
	- year, length $\rightarrow$ year
	- year, length $\rightarrow$ year, length

#### Implication: 
- a FD  $A \rightarrow B$  follows from a set of FDs S
- i.e., S logically implies $A \rightarrow B$ (written as $S \models A \rightarrow B$)
- if every relation instance that satisfies all the FDs in S also satisfies:           $A \rightarrow B$
	- Example: $\{A \rightarrow B, B \rightarrow C\} \models A \rightarrow C$ (transitivity)
	- Example: $\{A \rightarrow B, C\} \models AC \rightarrow BC$ (augmentation)

- For sets of FDs S and T we write $S \models T$, if $S \models T$ for all $t \in T$ 
	-  $\{A \rightarrow B, B \rightarrow C, D\}$   $T=\{A D \rightarrow C D\}$  $\therefore S \models T$
 
#### Equivalence:
- S is equivalent to T, iff $S \models T$ and $T \models S$
	- S and T are satisfied by exactly the same relation instances
- A relation schema R satisfies a functional dependency (or a set of FDs), if every instance r of R satisfies it


# References