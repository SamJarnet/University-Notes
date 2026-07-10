2026-04-22 20:42

Status:

Tags: [[Modelling Concurrent Programs]]


# Modelling Concurrent Programs

#### Example
- Three processes (threads) running concurrently 
- Shared variable x 
- Assume the initial value of x is 0
	![[Pasted image 20260422204438.png]]
- Questions:
	- How many reachable processes does the program have?
		- 5407 - through model checking
	- How many ways to move between states does the program have?
		- 14378 - 3 x last answer
	- How many possible executions are there?
		- Infinite - each state can branch into multiple next states - there are cycles
		- State explosion problem 
	- Is x always between 0 and 200?
		- Yes - check 

#### A typical model checker
- ![[Pasted image 20260422205631.png]]

#### Model Checking - The Process
- 1. Modelling - build model of proram (e.g. transition system)
- 2. Specification: specify desired properties of the system in a suitable formalism (model annotations, temporal logic)
- 3. Verification (with model checker): 
	- Explore all possible executions to check if specified properties  hold 
		- E.g. all possible thread interleavings
	- Counter example (error trace) produced when model does not satisfy the specification 
		- Simulate counter example
		- Revise model/code and/or specification 

#### Model Checking in Practice
- Many model checkers work on actual software, not models
-  correctness properties can be generic (e.g. arithmetic overflow, array bounds, division by zero, pointer safety deadlock) or program specific (e.g. "value of x  is always between 0 and 200" or "value of x eventually reaches 100") 
- key problem: state space explosion 
	- number of program states is exponential in the number of variables
- Symbolic model checking: state space represented symbolically 
- bounded model checking: explore only up to a given depth
	- impact on correctness guarantees 

#### Model Checking Using SPIN
Promella:
	![[Pasted image 20260422210258.png]]
	![[Pasted image 20260422210320.png]]
- Fixed:
	![[Pasted image 20260422210348.png]]

#### Transition Systems as Models of Systems 
- Modelling a system amounts to identifying:
	- its internal state at any time 
	- which state(s) it each state can transition into.
- Informally, transition systems are graphs 
	- nodes represent system states
	- edges represent atomic state changes 
	- states labelled with relevant properties 
	- paths correspond to system runs 
- e.g. traffic light model:
	![[Pasted image 20260422210605.png]]


#### Transition Systems
- We use a set Prop of atomic propositions to describe basic properties of states
	- e.g. Prop = {red, amber, green}
- A transition system T over Prop is given by:
	- a finite set $S$ of states
	- a subset $S_0 \subseteq S$ of initial states
	- a transition relation $R \subseteq S \times S$ between states
	- A valuation $V:S \rightarrow P$ (Prop) giving, for each state $s \in S$, the atomic propositions which are true in that state $V(s) \subseteq$ Prop
- Example:
	![[Pasted image 20260422210925.png]]

#### Transition Systems as Models of Programs
- States model program states
	- Values stored in all memory (stack/heap)
	- Value of program counter
- Transition model atomic computation steps (arising from executing atomic program statements)
- Atomic propositions describe basic properties of states (e.g. values of program variables)
- Maximal paths (i.e. paths that cannot be extended further) starting in an initial state corresponding to possible program executions
#### Extracting Models from Sequential Programs - Example
- ![[Pasted image 20260422211558.png]]

#### Extracting Models from Concurrent Programs - Example
- ![[Pasted image 20260422211739.png]]
- ![[Pasted image 20260422211753.png]]

#### The Behaviour of a Transition System
- Possible behaviours arise as follows:
	- nondeterministically select an initial state $s$ 
	- while $s$ has outgoing transitions:
		- nondeterministically select a transition $s \rightarrow s'$ 
		- execute the corresponding action 
		- let $s = s'$ 
	- Systems executions are maximal sequences
		- $s_0 \rightarrow s_1 \rightarrow s_2 \rightarrow ...$ 
		- (can be finite or infinite)

#### Modelling Concurrent Programs
- We will look at concurrent programs:
	- Several processes/threads executing concurrently 
	- communication through shared variables 
	- usual sequential constructs: assignments, if, while, skip, ...
	- concurrency primitives: e.g. wait, lock, unlock statements 
- Example:
	![[Pasted image 20260422213045.png]]
- cobegin  ... coend specifies concurrent execution 
- wait (c) repeatedly tests condition c, proceeds when true 
#### Why Model Checking?
- Simple mutual exclusion protocol:
	![[Pasted image 20260422213348.png]]
- Can use a model of this program to check:
	- Can the program reach a state where both $P_0$ and $P_1$ are using the shared resource? (this would violate mutual exclusion)
	- Does there exist an execution of the program where $P_1$ never accesses the shared resource?
- Note: shared code has no influence on above properties provided it terminates and does not modify turn!

#### Adding Program Counters
- How do we represent such programs using transition systems?
	- Start by identifying the unique entry and exit points of each atomic program statement, e.g.
		![[Pasted image 20260422213657.png]]
	- For sequential programs, we define a recursive procedure for annotating a program with entry points of atomic program statements.
	- Note: if and while statements are not atomic 

#### The annotation procedure for sequential programs 
- If P is not a composite statement (e.g. P is an assignment, skip, wait, lock, unlock), do nothing: 
	- -$P^L=P$ 
- If $P = P_1; P_2$: 
	- $P^L = $P_1^L;I:P_2^L$ 
- If $P=$ if (b) $P_1$ else $P_2$:
	- $P^L =$ if (b)$I_1:P_1^L$ else $I_2:P_2^L$ 
- If $P =$ while(b){$P_1$}:
	- $P^L =$ while(b){$I_1:P_1^L$}
- At the end, add labels for the entry and exit points of the program itself.
- Example: Basic mutual exclusion protocol:
	![[Pasted image 20260422214427.png]]

#### The annotation procedure
- ![[Pasted image 20260422214527.png]]
- Note:
	- exit points of concurrent processes also need to be labelled
	- no two labels must be identical

#### Example: Basic Mutual Exclusion Protocol
- ![[Pasted image 20260422214752.png]]
- Extract a transition system which models P: 
	- States are determined by the program counters of $P_0$ and $P_1$, together with the value of the shared variable turn
	- Transitions correspond to atomic execution steps in one of the processes (execution of processes is interleaved)
	- Prop and V extracted from states
- The model:
	![[Pasted image 20260422215002.png]]

#### Extracting Transition Systems from Concurrent Programs
- Outline of general procedure:
	- annotate the entry and exit points of basic program statements with process counters 
	- the states of the transition system are tuples consisting of:
		- the values of global variables 
		- the values of local process variables
		- the values of process counters
	- transitions between states correspond to individual atomic steps in one of the processes 
	- atomic propositions take the following forms:
		- var = v with var a program variable and v a possible value for var
		- $PC_i = I$ with $i$ a process and $I$ the entry point of a statement in process $i$ 
			- so $n_0$ in the diagram is a shorthand for $PC_0 = n_0$ 

#### Correctness Properties 
- Can the program reach a state where both $P_0$ and $P_1$ access the shared resource?
	- suffices to check for states $s$ with $V(s) ∋ PC_0 = c_0, PC_1 = c_1$
- Does there exist an execution of the program where $P_1$ never accesses shared resource?
	- Suffices to check for paths that never reach states $s$ with $V(s) ∋ PC_1 = c_1$ 
- We can verify program properties by exploring the graph
	![[Pasted image 20260422215958.png]]


# References