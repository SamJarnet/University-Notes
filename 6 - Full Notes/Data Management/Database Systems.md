29-10-2024 12:00

Status:

Tags: [[Data Management]] [[Structured Data]]


# Database Systems

#### Keys:
- A set of attributes forms a key for a relation if we do not allow two different tuples in a relation instance to have the same values in all the attributes of the key
- Courses(<u>CourseID</u>, Name, DeptID)
- Students(Name, Surname)
- Name and surname are not good for keys as they are unlikely to be unique, could combine to make a key (may break)

#### Functional Dependencies:
- Let a relation with schema R($A_1$, …, $A_n$, $B_1$, $B_2$, …., $B_m$) and let r an instance of R
- We say that r satisfies the functional dependency 
	- $A_1$, …, $A_n$  $\rightarrow$  $B_1$, $B_2$, …., $B_m$ if 
		- whenever two tuples in r agree on the values $A_1$, …, $A_n$ then they also agree on the values of $B_1$, $B_2$, …., $B_m$ 
		- in other words, there are no two tuples in r that have the same value on the attributes of $A_1$, …, $A_n$ , but differ on the values $B_1$, $B_2$, …., $B_m$
- We say that $A_1$, $A_2$, …, $A_n$ functionally (or uniquely) determines $B_1$, $B_2$, …., $B_m$
- $A_1$, $A_2$, …, $A_n$ is the determinant and  $B_1$, $B_2$, …., $B_m$ is the dependant set
- If X and Y are sets of attributes of schema R, then we write X → Y to denote the FD with the members of X in the left-hand side and the members of Y in the righthand side
	- if A= {$A_1$,…,$A_n$} and B= {$B_1$,$B_2$,...,$B_m$} and $A_1$,…,$A_n$→ $B_1$,$B_2$,...,$B_m$ then we write A→ B
Example:
![[Pasted image 20241029131453.png]]

[[Rules for Functional Dependencies]]

#### How do we know that some FDs hold for a database/relation schema?
- This question is all about instances
- With the information that is provided by the schema designer a FD may be derived (logically implied) from other known FDs about the schema
- With a given instance r, we can only derive information about FDs that do not hold on the schema (and not about FDs that hold on the schema)

#### Superkeys:
- For a relation schema R, X a set of attributes R
- X is a superkey of R if $X \rightarrow A_i$ for every attribute $A_i$ of $R$ 
- Every relation has at least one superkey (the set of all attributes)



# References