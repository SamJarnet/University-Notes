2026-04-28 13:10

Status:

Tags: [[Promela]] [[Formal Specification and Verification]]


# SPIN Verification

#### Correctness Properties - System Design perspective
- Safety: properties that the system may not violate (in any reachable state)
	- absence of deadlock
	- system invariants 
	- state properties at specific points in the execution 
- Liveness: properties that the system must satisfy, in every possible execution 
	- absence of livelock (the system makes progress infinitely often)
	- absence of starvation (a specific process makes progress infinitely often)
	- e.g. responsiveness 

#### Correctness Properties - System Verification perspective
- Verification is about determining whether design requirements could possibly be violated by examining all possible executions 
- Claims about reachable/unreachable states (safety) 
	- check for executions that lead to violation of a safety property
- Claims about feasible/infeasible executions (liveness)
	- e.g. check for executions where progress can be postponed indefinitely 

#### SPIN Outline
- edit Promela models (+ syntax check)
- simulate Promela models:
	- random (with seed)
	- interactive (gives control on resolving nondeterminism) 
	- guided (based on error trace produced during verification)
- verify Promela models:
	- exhaustive search: all possible states/executions are explored (works for models with ~ 100,000 states)
	- high coverage approximation methods
	![[Pasted image 20260428132853.png]]

#### Types of Correctness claims
- Basic assertions: 
	- specify that certain properties must hold at certain points in the execution
- meta-labels: 
	- used to check for absence of deadlock/livelock/starvation 
- never claims:
	- describe (complex) behaviour that should never occur
		- LTL formulas
- Trace assertions: 
	- describe valid/invalid sequences of channel operations

#### Assertions Example
- Assertions check for invariant property at specified points only
	![[Pasted image 20260428133455.png]]

#### Assertions 
- Promela Statement 
	- assert(condition) 
		- evaluates condition. If false, an error is reported
- Always executable
- automatically checked in simulation mode; if false, execution stops with error message
- in verification mode (safety), full state space is searched for assertion violations

#### Assertions ABP
- should not be possible to reach else branch if protocol was correct 
	![[Pasted image 20260428133853.png]]
- So we use assert(false) instead of skip to check else branch is not reached

#### ABP modelling the data
- Sender randomly generates data to be sent 
	![[Pasted image 20260428134054.png]]
	![[Pasted image 20260428134100.png]]
	![[Pasted image 20260428134108.png]]

#### ABP - Verification 
- recvd variable used for verification only (control flow not affected)
- could have used atomic{...} to avoid additional transitions
	![[Pasted image 20260428134217.png]]

#### Verifying Invariants
- Check for invariance if property p through additional process:
	![[Pasted image 20260428134322.png]]
	- boolean expression p can only contain global variables 
	- all possible interleavings of model processes + check process explored, hence check for invariance
- more efficient way to verify invariants uses never claim:
	![[Pasted image 20260428134442.png]]
	- system and claim process execute in lockstep

#### Meta-Labels
- labels used in Promela as targets for goto statements but also for verification 
- Types of verification labels:
	- end labels: used to check for absence of reachable deadlock states
		- mark valid end states (where deadlock is acceptable) with special labels
	- progress labels: used to check for absence of livelock
		- mark progress states with special labels
	- accept labels:
		- used to check for absence of acceptance cycles (e.g. inside never claims)

#### End Labels (Semaphore)
- Semaphore:
	![[Pasted image 20260428134829.png]]
- Users:
	![[Pasted image 20260428134844.png]]
- Synchronous channel models semaphore 
- without end label, SPIN detects deadlock state
- but waiting at end label should not be viewed as error

#### End Labels 
- Have names that begin with end
- define additional valid end states
- implicitly, only valid end states are where every Promela process has reached the end of its code
- any invalid end state is a deadlock state
- in verification mode (safety), SPIN automatically checks for absence of reachable deadlock states.

#### Progress Labels (semaphore)
- Semaphore: 
	![[Pasted image 20260428135300.png]]
- Users:
	![[Pasted image 20260428135312.png]]
- successful passing of semaphore test interpreted as progress
- in all infinite executions, semaphore process must reach progress label infinitely often

#### Progress Labels
- used to check that infinite executions make progress infinitely often 
- have names that begin with progress
	- identify states where progress was made
- non-progress cycle: execution cycle that does not pass through any progress state
	- if such cycle exists, repeating it infinitely yields execution without progress
	- conversely, if an infinite execution without progress exists, there must exist such cycle (as number of states is finite)
- In verification mode (liveness), SPIN can check absence of non progress cycles
	- i.e. that all infinite executions visit progress label infinitely often

#### Progress Labels (ABP)
- Sender:
	![[Pasted image 20260428135926.png]]
- Daemon: 
	![[Pasted image 20260428135946.png]]
	- Sender should receive ack infinitely often
	- progress labels checks this 
	- with Daemon process present, SPIN detects non-progress cycle

#### Fairness
- Fairness assumptions often needed to verify correctness 
	- e.g. need to assume that messages are not continuously lost
- finite progress assumption: any process that can execute a statement will eventually do so
	- in concurrent environment, this captures fairness of process scheduler
	- in distributed environment, it simply says that any process will eventually execute an executable statement
- Variants of the finite progress assumption:
	- weak fairness assumption: a statement which becomes enabled which becomes and remains enabled thereafter will eventually be scheduled
		- e.g. if a message is continuously available on Receiver's input channel, it will eventually be picked up by Receiver
	- strong fairness assumption: if a statement is enabled infinitely often, it will eventually be scheduled
		- e.g. if a message becomes available infinitely often on the Receiver's input channel, it will eventually be picked up by Receiver.
- In verification mode, only weak fairness can be assumed
	- verifier only explores weakly fair executions

#### Fairness Example
- Sender:
	![[Pasted image 20260428135926.png]]
- Daemon: 
	![[Pasted image 20260428135946.png]]
	- Without weak fairness, non progress cycles detected (daemon can steal messages indefinitely)
	- also with weak fairness enforced, non progress cycles exist

#### Summary of Correctness claims
- assertion checks mutual exclusion 
- end label indicates that blocking here is acceptable 
- progress label checks absence of livelock

- basic assertion: 
	- "some condition must hold at certain points in the execution of a process" 
- end-state label: 
	- "it is impossible for the system to terminate without all active processes having either terminated or stopped at identified end states" 
- progress-state label:
	- "it is impossible for the system to execute forever without passing through at least one specially identified progress states infinitely often"
# References