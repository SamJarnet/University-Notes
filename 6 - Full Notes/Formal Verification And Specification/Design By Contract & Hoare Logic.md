2026-04-20 20:28

Status:

Tags: [[Formal Specification and Verification]]


# Design By Contract & Hoare Logic

#### DbC 
- A contract protects both sides:
	- Client: specifies how much should be done 
	- Contractor: specifies how little is acceptable 
- Principle:
	- Method/Class that provides some functionality, it may:
		- Expect a certain condition to hold on entry (the precondition)
		- Guarantee a certain property on exit (the post-condition)
		- Maintain a certain property during execution (the invariants)
	- Preconditions, postconditions and invariants are assertions

#### Pre/Post-conditions
- Precondition: properties assumed to be true before the method execution
	- Precondition as Assumption
	- The contractor can assume that the precondition hold when implementing the method
	- If the method receives inputs which violate the preconditions, then it has no obligation to do anything sensible
- Postcondition: properties that a method must achieve after it completes
	- Postcondition as Obligation
	- The postcondition describes the method contractual obligation 
	- The contractor must deliver the postcondition to the client 

#### Example precondition
- ![[Pasted image 20260420203947.png]]

#### Example Postcondition
![[Pasted image 20260420204014.png]]


#### Hoare Triple 
- $\{P\}S\{Q\}$
- $P$ is the precondition
- $S$ is the program
- $Q$ is the postcondition
- Meaning:
	- $S$ will establish $Q$ on completion provided that $P$ holds before the execution of $S$ 
		- This is called partial correctness, $S$ does not have to terminate

#### Hoare Triple Examples 
![[Pasted image 20260420204153.png]]

#### New and Old Variables
- In a postcondition 
	- old(x) refers to the value of x before the execution 
	- x refers to the value of x after the execution 
		- postconditions are a before-after predicates
- Examples:
	![[Pasted image 20260420204503.png]]

#### A Simple Programming Language
- Assignment: x := E;
	- Parallel assignment x, y := E, F;
- Sequential Composition: S;T 
- Conditional Statement: if P {S;} {T;}
- While loop: while P {S}

#### Rule of Assignment 
- ![[Pasted image 20260420204757.png]]
- $P[x:= E]$ is the result of substituting E for any free occurrences of x in P
- Bound variables:
	- variables under quantifications, e.g. $\forall, \exists$ 
- Free variables:
	- variables not under quantification
- x is bound in $∀x.x > 0 → x > y$ 
- y is free in $∀x.x > 0 → x > y$ 
- Example:
	![[Pasted image 20260420205017.png]]
	![[Pasted image 20260420205046.png]]
	![[Pasted image 20260420205113.png]]

#### Old Variables
- ![[Pasted image 20260420205133.png]]
- $P[x, old(x) := E, x]$ is the result of substituting E and x for any free occurrences of x and old(x), respectively in P
- Example
	![[Pasted image 20260420205238.png]]

#### Parallel Assignment 
- ![[Pasted image 20260420205303.png]]
- $P[x, y := E, F]$ is the result of substituting E and F for any free occurrences of x and y, respectively in P
- Example:
	![[Pasted image 20260420205335.png]]

#### Rule of Consequence 
- How can we prove the validity of {x > 2} x := x + 1 {x > 3}
- ![[Pasted image 20260420205417.png]]
- Precondition weakening 
- Postcondition strengthening 
- Example:
	![[Pasted image 20260420205445.png]]

# References