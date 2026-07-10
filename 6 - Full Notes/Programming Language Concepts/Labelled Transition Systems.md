2026-04-18 13:53

Status:

Tags: [[Programming Language Concepts]]


# Labelled Transition Systems

#### Complex Semantics 
- When it comes to understanding a concurrent program we must consider each of its threads and the semantics of each thread can be represented as a tree of behaviours
- When considering whether an implementation of a particular thread meets its semantics we must have a means of considering 
	- the actual behaviour of a thread (as a tree of actions) and 
	- the specified semantics (as a tree of actions) 
- We need a way of comparing trees of actions 
- The particular forms of trees we use are represented as graphs of labelled actions and are referred to as labelled transition systems

#### Reasoning about concurrent programs
- These are some essential aspects of concurrency that make it different from sequential computation e.g.:
	- communication - processes communicate with other processes either through shared memory or with messaging passing
	- synchronisation - processes must sometimes synchronise their actions to ensure atomicity
	- nondeterminism - what can be observed about a program changes from one run to the next 
- Some thins that we take for granted need to be rethought: e.g. how to test concurrent code?

#### Nondeterminism example
- Suppose we run the above three pieces of pseudocode concurrently.
- What will be printed?
	![[Pasted image 20260418140210.png]]
- x is "0" or x us "1" or x is "2" 

#### Possibilities 
- We can use a mathematical structure called a LTS in order to capture what can be observed about programs 
	- LTS are a mathematical structure for reasoning about nondeterminism
	- the labels of transitions say "what can be observed" 
	- e.g.
		![[Pasted image 20260418140404.png]]

#### Labelled Transition Systems
- An LTS is a mathematical structure $(X, \Sigma, L)$ where 
	- $X$ is a set of states
	- $\Sigma$ is an alphabet of actions 
	- $L \subseteq X \times \Sigma \times X$
- X is {0,1,2,3} - say
- Σ is {"x is 0", "x is 1", "x is 2"} 
- L is { (0,"x is 0",1), (0,"x is 1",2), (0,"x is 2",3) }
- We write $x \xrightarrow{a} y$ to mean $(x, a, y) \in L$ 
	![[Pasted image 20260418140628.png]]

#### LTSs and finite state automata 
- Labelled transition systems are similar to finite state automata, which also have states and transitions, but there are important differences.
	- The set of states in an LTS can be infinite: we cannot assume that our systems have only a finite number of possible states
	- LTSs typically do not have initial and final states

#### Kinds of nondeterminism 
- Internal - "the machine chooses" 
	- e.g. the simple code example we have examined 
	- the nondeterminism is resolved by the scheduler 
- External - "the environment chooses" 
	- e.g. interactive systems such as vending machines
	- the combination of a vending machine and user can be thought of as a concurrent system

#### External nondeterminism - Vending machine 
- The user puts in money - this is the £ action
- The machine now offers a choice between tea (t) and coffee (c) 
	![[Pasted image 20260418141511.png]]

#### Process equivalence 
- Non determinism is inherent in concurrent and interactive systems 
- What does it mean that a system is correct
	- One answer: it should behave like (be equivalent to) some specification 
	- But what should equivalent mean?

#### First Try
- Give the specification as a set of traces
	- A trace is a sequence of observations from state
	- example:
		![[Pasted image 20260418141741.png]]
- Say that two states are trace equivalent when they have the same set of all traces possible 

#### Traces, Example
- Some systems have an infinite set of traces
	![[Pasted image 20260418141937.png]]
- Traces from $x_0$ are 
	- { $ε, a, b, aa, ab, aaa, aab, aaaa, aaab, aaaaa, aaaab, ….$ }
- Indeed, empty and all the words matched by the regular expression $a^*b$ 

#### Example: vending machines 
- Should we consider these two vending machines as equivalent?
	![[Pasted image 20260418142254.png]]
- Are they trace equivalent?
	- Yes, but we should probably not consider them equivalent - deadlock and branching issues

#### Moral
- In some cases, trace equivalence is too coarse: it equates too much
	- we want to distinguish the two vending machine examples
# References