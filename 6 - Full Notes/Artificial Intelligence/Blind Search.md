2025-12-03 12:29

Status:

Tags: [[Artificial Intelligence]]


# Blind Search

#### Problem Types
- Deterministic, fully observable -> Single-State problem
	- Agent knows exactly which state it will be in; solution is a sequence
- Non-observable -> Sensorless problem
	- Agent may have no idea where it is; solution is a sequence
- Nondeterministic and/or partially observable -> contingency problem
	- Percepts provide new information about current state
	- Often interleave search, execution
- Unknown state space -> Exploration Problem

#### Single-State problem Formulation
- A problem is defined by four items:
	- Initial state e.g. location
	- Actions or successor function $S(x)=$ set of action-state pairs
		- e.g. $S(Arad) = \{<Arad \rightarrow Zerind, Zerind>, … \}​$
	- Goal test, can be
		- Explicit, e.g. x=location
		- Implicit e.g. Checkmate(x)
	- Path cost (additive)
		- e.g. sum of distances, number of actions executed, etc.
		- $c(x,a,y)$ is the step cost, assumed to be $\geq 0$ 
	- A solution is a sequence of actions leading from the initial state to a goal state

#### Selecting a State Space
- Real world is complex
	- State space must be extracted for problem solving
- Abstract state = set of real states
- Abstract action = complex combination of real actions
	- e.g., "$Arad \rightarrow Zerind$" represents a complex set of possible routes, detours, rest stops, etc. ​
- Abstract solution = 
	- Set of real paths that are solutions in the real world
- Each abstract action should be easier than the original problem

#### Tree Search Algorithms 
- Basic idea:
	- Offline, simulated exploration of state space by generating successors of already-explored states (a.k.a. expanding states)

#### Implementation: States vs Nodes
- A state is a representation of a physical configuration 
- A node is a data structure constituting part of a search tree includes state,parent node, action, path cost $g(x)$, depth
- State and nodes aren't the same 

#### Search Strategies
- A search strategy is defined by picking the order of node expansion
- Strategies are evaluated along the following dimensions:
	- Completeness: Does it always find a solution if there is one?
	- Time complexity: number of nodes generated 
	- Space complexity: maximum number of nodes in memory 
	- optimality: does it always find a least-cost solution?
- Time and space complexity are measured in terms of:
	- b: maximum branching factor of the search tree
	- d: depth of the least-cost solution
	- m: maximum depth of the state space (may be inf)
- Uninformed search strategies:
	- Use only the information available in the problem definition:
		- Breath first
		- Depth first
		- Depth limited
		- Iterative Deepening

#### Breadth First Search
- Expand shallowest unexpanded node:
- Implementation:
	- Fringe is a FIFO queue, i.e. new successors go at the end 
- Complete if b is finite
- TC = $O(b^{d+1})$
- SC = $O(b^{d+1})$ (keeps every node in memory)
- Optimal if cost = 1 per step

#### Depth First Search
- Expand deepest unexpanded node:
- Implementation:
	- Fringe is a LIFO queue, i.e. new successors put at front
- Not complete in infinite depth spaces, spaces with loops
	- Modify to avoid repeated states along path
		- Complete in finite space
- TC = $O(b^{m})$ bad if $m$ is much larger than $d$ 
	- if solutions are dense, may be faster than breadth first
- SC = $O(bm)$ linear space
- Not optimal

#### Depth-Limited Search
- Depth first with depth limit $n$ 
- i.e. nodes at depth $n$ have no successors

#### Iterative Deepening Depth-First Search (IDDFS)
- Combines the space efficiency of DFS with the optimality and completeness of BFS
- Expands shallowest nodes first in terms of depth limit, but within each iteration uses DFS
- Repeatedly runs Depth-Limited Search with increasing depth limits:
    - First limit = 0
    - Then 1, 2, 3, … until solution is found
- Implementation:
    - Uses DFS with a depth limit
    - Restart search each time with limit increased by 1
    - Order of expansions:
        - Within each iteration → LIFO (like DFS)
        - Across iterations → effectively FIFO by depth (like BFS)
- Complete if:
    - Branching factor is finite
    - Solution depth is finite
- TC = $O(b^d)$
    - Re-expands nodes at shallow depths multiple times
    - Overhead is small because most nodes are near depth $d$
- SC = $O(bd)$
    - Stores only one DFS path at a time
    - Much less memory than BFS
- Optimal if:
    - Cost = 1 per step
    - Like BFS, finds shallowest solution first

#### Repeated States 
- Failure to detect repeated states can turn a linear problem into an exponential one
	![[Pasted image 20251203125537.png]]

#### Bidirectional Search
- Do two searches
	- One starts from the initial state
	- One starts from the goal state
- Motivation:
	- $b^{d/2}+b^{d/2}$ is much less than $b^d$ 
- At each iteration of each search:
	- Check if a node is in the fringe/open of the other before expansion
	- If yes, a solution has been found 

# References