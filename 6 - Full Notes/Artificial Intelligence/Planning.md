025-12-03 21:56

Status:

Tags: [[Artificial Intelligence]]


# Planning

#### What is planning? 
- Generate and search over possible plans: sequences of actions to perform tasks and achieve objectives.
	- States, actions and goals 
- Classical planning environment: fully observable, deterministic finite static and discrete.
- Assists humans in practical applications
	- Design and manufacturing
	- Military operations
	- Games
	- Space exploration 

#### Difficulty of real world problems
- Which actions are relevant?
	- Exhaustive search vs backward search
- what are good heuristic functions?
	- Good estimate of the cost of the state
	- Problem dependent vs problem independent
- How to decompose the problem?
	- Most real world problems are nearly decomposable 

#### Planning Language
- What is a good language?
	- Expressive enough to describe a wide variety of problems 
	- Restrictive enough to allow efficient algorithms to operate on it 
	- Planning algorithm should be able to take advantage of the logical structure of the problem

#### General Language Features
- Representation of states
	- Decompose the world in logical conditions and represent a state as a conjunction of positive literals.
		- Proposition literals: $Poor \land Unkown$
		- FO-Literals (grounded and function free): $At(Plane1, Melbourne) \land At(Plane2, Sydney)$ 
		- Closed world assumption
	- Representation of goals
		- Partially specified state and represented as a conjunction of positive ground literals
		- A goal is satisfied if the state contains all literals in goal.
- Representation of actions: Action = Precondition + Effect
	- Action: Fly(p, from, to)
	- Precondition: At(p, from) $\land$ Plane(p) $\land$ Airport(from) $\land$ Airport(to)
	- Effect: $\neg$ At(p, from)  $\land$ At(p,to)
- Action schema ("p", "from", "to" need to be instantiated)
	- Action name and parameter list 
	- Precondition (conjunction of function-free literals)
	- Effect (conjunction of function-free literals)
- Add-list vs delete-list

#### Language semantics?
- How do actions affects states?
	- An action is applicable in any state that satisfies its precondition
	- For first-order action schema, applicability involves a substitution $\theta$ for the variables in the precondition 
		![[Pasted image 20251223174122.png]]

- The result if executing action $a$ in state $s$ is the state $s'$
	- $s'$ is the same as $s$ except:
		- Any positive literal $P$ in the effect of $a$ is added to $s'$ 
		- Any negative literal $\neg P$ is removed from $s'$ 
		- Effect:
			![[Pasted image 20251223174431.png]]
	- STRIPS assumption: (avoids representational frame problem)
		- Every literal not in the effect remains unchanged

#### Expressiveness and extensions
- STRIPS is simplified: function free literals 
	- Allows for propositional representation
	- Function symbols lead to infinitely many states/actions 
- Extension: Action Description Language (ADL)
- Allows negative literals and disjunctions (or)
	![[Pasted image 20251223174825.png]]
- Standardisation: Planning Domain Definition Language (PDDL)

#### Example: Air Cargo Transport
``
	![[Pasted image 20251223174942.png]]


#### Example: Blocks World
``
	![[Pasted image 20251223175051.png]]

#### Planning with state-space search
- Both forward and backward search possible 
- Progression planners 
	- Forward state-space search
	- Consider the effect of all possible actions given state
- Regression planners
	- Backwards state-space search
	- To achieve a goal, what must have been true in the previous state

#### Progression Algorithm 
- Formulation as state-space search problem:
	- Initial state = initial state of the planning problem 
		- Literals not appearing are False
	- Possible Actions = those with satisfied preconditions 
		- Add positive effects, delete negative
	- Goal test = does the state satisfy the goal
	- Step cost = each action costs 1
- No functions, any graph search that is complete is a complete planning algorithm, e.g., $A^*$

#### Regression Algorithm 
- How to determine predecessors?
	- Which states are immediately prior to the goal?
		- Goal state = ![[Pasted image 20251223175645.png]]
		- Relevant actions for the first conjunct: $Unload(C_1, p, B)$
		- Works only if pre-conditions are satisfied 
		- Previous state=  
		 ![[Pasted image 20251223175807.png]]
		- (Subgoal $At(C_1, B)$ should not be present in this state)
- Actions must not undo desired literals (consistent) 
- Main advantage: only relevant actions are considered.
	- Often much lower branching factor than forward search

- General process for predecessor construction 
	- Give a goal description $G$ 
	- Let $A$ be an action that is relevant and consistent
	- The predecessors is as follows:
		- Any positive effects of $A$ that appear in $G$ are deleted
		- Each precondition literal of $A$ is added, unless it already appears.
- Any standard search algorithm can be added to perform the search
- Termination when predecessor satisfied by initial state

#### Heuristics of state-space search
- Neither progression nor regression are very efficient without a good heuristic 
	- How many actions are needed to achieve the goal?
	- Exact solution is NP hard, find a good estimate
- Two approaches to find admissible heuristic:
	- The optimal solution to the relaxed problem 
		- Remove all preconditions from actions 
	- The sub-goal independence assumptions
		- The cost of solving a conjunction of sub-goals is approximated by the sum of the costs of solving the sub-problems independently.

#### Partial-Order Planning
- Progression and regression planning are totally ordered plan search forms.
	- They cannot take advantage of problem decomposition
	- Decisions must be made on how to sequence actions on all the subproblems
- Least commitment strategy:
	- Delay choices (that don't need to be made yet) during construction of the plan

#### Shoe Example
``
	![[Pasted image 20251223181508.png]]

#### POP
- Any planning algorithm that can place two actions into a plan without fixing which comes first is a PO plan.
	![[Pasted image 20251223181738.png]]

#### Why search in POP space rather than F(ully)OP space?
- When sub-goals are semi-independent, the number of fully-ordered plans can be exponentially more than the number of partially ordered plans
- Thus searching in space of POPs is much more efficient (much smaller search space) than searching in space of FOPs. (And, when they are not independent, its not significantly worse)
- Secondarily, there is flexibility when executing the plan.


# References