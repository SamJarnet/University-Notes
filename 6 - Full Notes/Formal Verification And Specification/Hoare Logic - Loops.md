2026-04-20 21:23

Status:

Tags: [[Formal Specification and Verification]]


# Hoare Logic - Loops

#### A More Compact Representation 
- Proof for: {x > 2} x := x + 1 {x > 2}
	- ![[Pasted image 20260420212507.png]]
- Indicate the rule and its dependency on each line 
- Numbering backward since we build the proof from the goal 

#### While Rule (Partial Correctness)
- ![[Pasted image 20260420212630.png]]
- $P$ is called the loop invariant 
- Example:
  ![[Pasted image 20260420212928.png]]![[Pasted image 20260420212936.png]]


# References