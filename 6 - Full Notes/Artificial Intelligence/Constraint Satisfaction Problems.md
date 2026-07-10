2025-12-31 12:37

Status:

Tags: [[Artificial Intelligence]]


# Constraint Satisfaction Problems

#### Standard Search Problem
- State is a "black box" - any data structure that supports successor function, heuristic function and goal test
- CSP:
	- State is defined by variables $X_i$ with values from domain $D_i$ 
	- Goal test is a set of constraints specifying allowable combinations of values for subsets of variables 
	- E.g. Graph colouring, N-Queens
- Simple example of a formal representation language
- Allows useful general-purpose algorithms with more power than standard search algorithms

#### Map Colouring 
- ![[Pasted image 20251231124052.png]]

- Solutions are complete and consistent assignments, e.g., WA = red, NT = green,Q = red,NSW = green,V = red,SA = blue,T = green​

#### Constraint graph
- Binary CSP: each constraint relates two variables 
- CG : nodes are variables, arcs are constraints
- ![[Pasted image 20251231124219.png]]
- Colouring can be usedf for bandwith assignment in mobile phone masts 

#### Varieties of CSPs 
- Discrete variables:
	- Finite domains:
		- n variables, domain size $d \rightarrow O(d^n)$ complete assignments 
		- e.g. boolean CSPs, ubclude boolean satisfiability (NP-Complete)
	- Infinite domains:
		- Integers, strings, etc
		- e.g. job scheduling, varaibles are start/end days for each job
		- need a constraint language e.g.:
			- ![[Pasted image 20251231124413.png]]
- Continuous variables 
	- e.g. start/end times for hubble space telescope observations
	- linear constraints solvable in poly time by linnear programming 

#### Varieties of constraints
- Unary constraints involve a single variable 
	- e.g. SA $\neq$ green
- Binary constraints involve pairs of variables
	- e.g. SA $\neq$ WA
- Higher-order constrains involve 3 or more variables
	- e.g. cryptarithmetic column constraints

#### Real world CSPs
- Assignment problems
	- e.g. whos teaching the class
- timetabling problems
	- e.g. which class is offered when and where
- Transportation scheduling 
- Factory scheduling 

#### Standard search formulation (incremental)
- States are defined by the values assigned so far
- Initial state: the empty assignment {}
- Successor function: assign a value to an unassigned variable that does not conflict with current assignment -> fail if no legal assignments
- Goal test: the current assignment is complete 

- This is the same for all CSPs 
- Every solution appears at depth n with n variables -> use depth first search
- Path is irrelevant, so can also use complete-state formulation
- $b= (b-l)d$ at depth $l$, hence num of leaves = $n!d^n$, even though there are only $d^n$ assignments 

#### Backtracking search
- Variable assignments are commutative, i.e. WA = red then NT = green  same as  NT = green then WA =red 
- Only need to consider assignments to a single variable at each node
	- b = d and there are $d^n$ leaves
- Depth first search for CSPs with single-variable assignments is called backtracking search
- Backtracking seach is the basic uninformed algorithm for CSPs 
- Can solve n-queens for n ~~ 25


#### Backtracking vs depth first search
- Very similar
- In DFS we assume that a node was expanded by applying all possible actions to add nodes to the fringe (then later if necessary these nodes will be on the fringe ready to be expanded further)
- Backtracking search just applies one action to produce one successor node, and continues on down (then later, if nec, on returning to this node it will check whether there are any other successors that can be generated) 

#### Improving backtracking efficiency 
- General purpose methods can give huge gains in speed
	- Which variable should be assigned next?
	- In what order should its values be tried
	- can we detect inevitable failures early 

#### Most constrained variable 
- Choose the variable with the fewest legal values 
- ![[Pasted image 20251231125843.png]]
- a.k.a minimum remaining values (MRV) heuristic
- because these are variables most likely to prune the search tree (e.g. consider a variable with no legal values remaining)

#### Most constraining variable
- Most constrained is a more import heuristic, but most constraining is a useful tie breaker among most constrained variables 
- Most constraining variable = the variable with the most constraints on the remaining variables 
- ![[Pasted image 20251231130042.png]]
- Because the variable involved in the most constraints -> is the most likely to cause a failure early/prune the search tree

#### Least constraining value 
- Given a variable, choose the least constraining value: 
	- The one that rules out the fewest values in the neighbouring variables - to leave other variables as open as possible
	- ![[Pasted image 20251231130240.png]]
	- Combining these heuristics makes 1000 queens feasible 

#### Forward Checking
- Idea:
	- Keep track of remaining legal values for unassigned variables 
	- Terminate search when any variable has no legal values
	- ![[Pasted image 20251231130410.png]]
	- Detects failure because no options remain for SA

#### Arc consistency 
- Simplest form of propagation marks each arc consistent 
- $X \rightarrow Y$ consistent iff for every value x of X there is some allowed y 
- If X loses a value, neighbours of X need to be rechecked 
- ![[Pasted image 20251231130621.png]]

#### Local Search for CSPs
- Hill-climbing, simulated annealing typically work with "complete" states i.e. all variables assigned 
- To apply to CPSs:
	- allow states with constraint violations 
	- operators reassign variable values
- Variable selection: randomly select any conflicted variable 
- Value selection by min-conflicts heuristic 
	- Choose value that violates the fewest constraints 
	- i.e. hill climb with $h(n)$ = total number of violated constraints

#### 4 Queens
- ![[Pasted image 20251231130854.png]]

#### Iterative Min-Conflicts 
- While we are not at a solution:
	- Choose a random conflicted variable 
	- Pick a value for this that has minimum conflicts 
- Works surprisingly well (On N-Queens)!
	- For n-queens, almost independent of problem size - due to dense solution space
	- Also works on scheduling problems 
		- Note: no need to restart and re-run backtracking 



# References