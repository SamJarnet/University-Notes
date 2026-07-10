2026-04-17 14:22

Status:

Tags: [[Programming Language Concepts]]


# Type Safety

#### A Statement of Type Safety 
- Well-typed programs never go wrong
	- We understand what it means to be well-typed for a program: inductive typing relation between programs and types
	- We know what it means for a program to "go" by inductively defining operational semantics for that program
- We need to understand what "wrong" means 
- Notice that the operational semantics we gave for the Toy language did not depend son the terms being well typed.
	- e.g. if(if(true) then false else 0) then true else 34 is ill-typed but according to the big and small step semantics, it would evaluate to the value 34.
	- consider if(if(false) then false else 0) then true else 34. This term is also ill-typed but if you evaluate it, it gets stuck
		![[Pasted image 20260417142608.png]]

#### Stuck Terms and Divergence 
- For the small step semantics, we can model our runtime errors as "stuck" terms. That is, terms that cannot evaluate any further and are not values of the language. 
-  For the big step semantics, we could do the same, but unfortunately, were we to introduce recursion or while loops to the language then big step semantics could not distinguish between stuck and divergent terms.
	- To model runtime errors in a big step semantics we must explicitly model errors. This would be done by introducing an error relation $E ↯$ that describes when $E$ has reached an error state.
	- e.g. if (n) then $E$ else $E' ↯$ would hold for any literal n.
	- Won't go into detail about error cases, just assume $↯$ is defined
- This means that we could now distinguish between a stuck term and a divergent term in the big step semantics in the presence of recursion.
- Unfortunately, this still doesn't allow us to state type safety for the big step semantics.
- The big step semantics only considers "complete computations". It cannot refer to what happens during computation.
- All that we can easily specify with a big step semantics is a weak notion of type correctness: preservation

#### Preservation 
- A typed language satisfies (weak) preservation if the following holds: 
	- for all closed well-typed languages : 
		![[Pasted image 20260417143741.png]]
- This states that programs do not change their type after their runtime. More precisely it says that values that programs produce actually are of the expected type.
- For small step:
	- A typed language satisfies preservation if the following holds:
		![[Pasted image 20260417143901.png]]
- This states that, at every step of evaluation, programs do not change their type.

#### Progress 
- Preservation alone is not a sufficient property to describe type safety 
- It does not capture the fact that well-typed terms stay in semantically "good" states
- For example, if we have a (broken) type system that allows a stuck term to be well-typed, then this stuck term will trivially satisfy preservation.
	- There are no reductions from the stuck term so types are preserved.
- To capture type safety more fully we need to know that well-typed terms never become stuck
- This property is what we call progress
- A typed language satisfies progress if the following holds:
	 - For all closed well-typed terms E :  
		![[Pasted image 20260417144316.png]]
- Type Safety =  preservation and progress

#### Why Type Safety = Preservation + Progress
- Suppose $\vdash$ is a typing relation that satisfies both Preservation and Progress for the reduction relation $\rightarrow$ 
- Suppose also that $E$ is a well typed expression such that $\vdash E : T$ 
- We need to show that $E$ never reaches error state.
	- Step 1. If $E$ is a value then go directly to step 4. Otherwise, by Progress, we know there must be some expression $E'$ such that $E \rightarrow E'$ 
	- Step 2. Because $\vdash E : T$ and because $E \rightarrow  E'$, then by Preservation we must have $\vdash E' : T$ for the same type $T$
	- Step 3. Go to Step 1 replacing $E$ with $E'$
	- Step 4. $E$ is a value so the program has successfully terminated
 - By repeatedly applying Progress, then Preservation, we guarantee that the program never reaches an error state.

#### Proving Progress for Toy Lambda
- Theorem: 
	- if $⊢ E : T$ then $E → E’$ or $E$ is a value $V$
- Proof: 
	- We use proof by induction over the typing derivation $\vdash E : T$ 
- Base Cases:
	- If the proof trees consist of just the rule TInt or TBool then $E$ is a value
- Inductive Cases (TIf as example):
	- Suppose the last rule used to derive the type of $E$ is TIf. Then we know that $E$ is of the form: if $E_1$ then $E_2$ else $E_3$ where $⊢ E_1 :$ Bool and $⊢ E_2 , E_3 : T$.
	- Now, if $E_1$ is not a value, then by the inductive hypothesis we must have that $E_1 \rightarrow E_1'$ for some $E_1$'. This allows us to derive: if $E_1$ then $E_2$ else $E_3 →$ if $E_1’$ then $E_2$ else $E_3$ as required.
	- Suppose that $E_1$ is a value. We know that only types of type Bool are true and false. In either case we get a reduction.
		- if $E_1$ then $E_2$ else $E_3 → E_2$ or
		- if $E_1$ then $E_2$ else $E_3 → E_3$
	- This means, whatever the form of $E_1$, we have a reduction and hence Progress.
- We must consider every type rule in the language and perform similar reasoning in each case.

#### Proving Preservation for Toy
- Theorem: 
	- if $⊢ E : T$ and $E \rightarrow E'$ then $⊢ E' : T$ 
- Proof: 
	- We use proof by induction over the typing derivation $\vdash E : T$ 
- Base Cases:
	- Rule TInt or TBool, $E$ i a value so the hypothesis is trivially satisfied 
- Inductive Cases (TIf as example):
	- Suppose the last rule used to derive the type of $E$ is TIf. Then we know that $E$ is of the form: if $E_1$ then $E_2$ else $E_3$ where $⊢ E_1 :$ Bool and $⊢ E_2 , E_3 : T$.
	- Now, consider the possible reductions that can originate from $E$ : either
		- (i) It is a reduction of $E_1$ to some $E_1'$, that is $E \rightarrow E'$ (so that $E'$ is if $E_1'$ then $E_2$ else $E_3)$ or
		- (ii) $E_1$ is a boolean literal and if $E_1$ then $E_2$ else $E_3 \rightarrow E_2$ (or similar for $E_3$) so that $E'$ is $E_2$ (or $E_3$).
	- In case (ii), we know that both $E_2$ and $E_3$ have type $T$ so therefore $\vdash E' : T$ as required.
	- In case (i) we apply the inductive hypothesis to $E_1$. We know that $\vdash E_1:$ Bool and by induction, we see that $\vdash E_1':$ Bool also. Hence if $E_1'$ then $E_2$ else $E_3 :T$ as required

# References