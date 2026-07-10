2025-12-09 13:11

Status:

Tags: [[Space Complexity]] [[Theory of Computing]] [[NP Completeness]]


# PSPACE Completeness

#### Definition
- A language $B$ is PSPACE-Complete if:
	- $B$ is in PSPACE
	- Every language $A$ in PSPACE is polynomial-time reducible to $B$
- If $B$ only satisfies the second condition, it is called PSPACE-Hard

#### Why not poly-space reducible?
- We defined NP-Complete problems by using polynomial-time reductions
- Because we wanted the reduction to be easy compared to typical problems in NP
- If we used polynomial space here, then an easy solution for the problem we are reducing would not necessarily give us an easy solution to the problem we are reducing from

#### A PSPACE-Complete Problem: TQBF
- Let TQBF be the problem of deciding whether a fully quantified boolean formula is true:
	- TQBF = $\{⟨ϕ⟩ | ϕ$ is a true fully quantified boolean formula $\}$
	- Examples:
		![[Pasted image 20251209132646.png]]

#### SAT and TQBF
- Polynomial-time reduction from SAT to TQBF:
	- $ϕ → ∃x_1 . . . . ∃x_n.ϕ$ 
	- $ϕ ∈$ SAT iff $∃x_1 . . . . ∃x_n.ϕ ∈$ TQBF
- For $\phi$ a boolean formula over $x_1,...x_n$
- This makes TQBF NP=Hard

#### A PSPACE-Complete Problem: TQBF
- Theorem: 
	- TQBF is PSPACE-Complete
- Proof (only of TQBF $\in$ PSPACE):
	- Any fully quantified boolean formula can be rewritten by moving quantifiers to the beginning
		- May need to rename some variables, e.g.:
			- $∀x.((∀y.(x ∨ y)) ∨ (∃y.(x ∧ ¬y)))$ rewritten to
			- $∀x.∀y.∃z.((x ∨ y) ∨ (x ∧ ¬z))$
		- Can do the rewriting using linear space
	- We then need to decide using polynomial space if the new formula is true

- Recursive algorithm for TQBF: On input $⟨ϕ⟩$:
	- 1. If $\phi$ is of the form $∃x.ψ$, recursively call the algorithm on $ψ[0/x]$ and $ψ[1/x]$. If one of these accepts, accept; otherwise reject.
	- 2.  If $\phi$ is of the form $\forall x.ψ$, recursively call the algorithm on $ψ[0/x]$ and $ψ[1/x]$. If one of these accepts, accept; otherwise reject.
	- 3. If $\phi$ contains no quantifiers, evaluate it. If true, accept; o/w reject.
- Above uses $O(n+m)$ space (n = number of variables, m = size of $\phi$)
	- Each step in the recursion stores value of one more variable only
	- The evaluation in the base case uses linear space

#### Winning Strategies for Games
- Checking if $ϕ := ∀x.∃y.(x ∧ ¬y) ∨ (¬x ∨ y)$ same as playing a game:
	- Opponent (A) picks value for $x$ 
	- We (E) pick value for $y$ 
	- ...
	- If substituting the chosen values for $x$ and $y$ gives true, then E wins the play; otherwise A wins.
- Then $\phi$ is true iff E has a winning strategy

- Let $ϕ = ∃x_1.∀x_2...Qx_k .ψ$ 
	- Can view deciding $\phi \in$ TQBF as deciding a two-player game:
		- Player A selects values for $\forall$ variables,
		- Player E selects values for $\exists$ variables,
		- Order of play is the order of quantifiers in $\phi$,
		- When all values are chosen, $ψ$ is evaluated; if true, player E wins, otherwise player A wins
	- Let FORMULA_GAME = $\{⟨ϕ⟩ | E$ has a winning strategy in the formula game associated with $\phi\}$ 
	- Key observation:
		- $\phi \in$ TQBF iff $\phi \in$ FORMULA_GAME
	- Corollary:
		- FORMULA_GAME is PSPACE-Complete

#### Geography Game
- Players take turn naming cities
- Chosen city must begin with same letter than ended previous city
- Start with designated city 
- No repetitions allowed 
- Player who gets stuck loses the game
- Can model this with graph $G$: cities as nodes, valid moves as edges
	- Valid plays are simple paths through the graph (paths which do not repeat nodes)
- The problem: does the first player have a winning strategy for the game $G$ starting at node $b$?

#### PSPACE-Hard Problems
- The geography game has a fixed board (fixed number of cities)
- Generalised geography game:
	- Played on an arbitrary directed graph with designated start node
	- Deciding this game is PSPACE-Complete
		- In PSPACE
		- PSPACE-Hard: this follows a reduction from TQBF
	- The number of moves is polynomial in the size of the board
		- Each recursive call removes a node from allowable moves
- Generalised chess: PSPACE-hard, believed not to be in PSPACE
- Generalised GO: PSPACE-hard, believed not to be in PSPACE
  
#### A Problem in EXPTIME and not in P
- In generalised geography, a play takes polynomial time in the size of the graph
- In generalised chess, a play may take exponential time in the size of the board
- The problem of evaluating a position in generalised chess is EXPTIME-complete, and not in P
	- Also largely believed not to belong to NP or PSPACE, although no one has proved this yet
  
  
  
  
  
  
  

# References