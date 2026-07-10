2026-04-28 11:15

Status:

Tags: [[Formal Specification and Verification]]


# Promela

#### SPIN 
- Simple Promela Interpreter
- efficient verifier implemented in C
- command line + GUI (ISPIN)

- Promela models describe (abstractions of) software systems
	- process interaction via shared variables and/or buffered channels 
	- models are bounded
- SPIN can be used to:
	-  validate (through simulations) Promela models
	- verify Promela models (full state-space exploration)
		- models represented using transition systems
	- partial verification of (very large) Promela models 

#### Example: Alternating Bit Protocol
- Simple network protocol that re transmits lost messages
	![[Pasted image 20260428111900.png]]
 - Sender tags message with addition bit, sends message and waits for acknowledgement with same bit value;
	 - on correct ack, it flips the bit and sends the message
	 - on incorrect/no ack, it resends message
- receiver acks messages by sending back bit value
- Main correctness property: 
	- Every message sent by S is received at least once, and accepted at most once by R

#### Promela
- The input language of the SPIN model checker
- verification modelling language (Process Meta-Language)
- not intended for general computation
- emphasis on control flow and coordination/synchronisation aspects of concurrent/distributed systems
	- communication through channels and/or global variables

#### Example: A Promela Model for Mutual Exclusion
- model describes transition system
	![[Pasted image 20260428112253.png]]
- processes P0, P1 compete for shared resource, must ensure mutually exclusive access
- correctness properties:
	- model annotations e.g. assertions 
	- temporal logic formulas e.g. "any state where turn == 1 is eventually followed by a state where turn == 0 "

#### Types of Objects in Promela
- processes: 
	- model the components of a system
	- have a global scope 
- data variables: 
	- global variables define the data environment for processes
	- local variables define internal process data
- message channels 
	- define communication environment for processes 
	- can have local or global scope 
	![[Pasted image 20260428112633.png]]

#### Data Objects
- Basic data types:
	![[Pasted image 20260428112713.png]]
- Enumerated data types:
	- used to declare (global) symbolic constants:
		![[Pasted image 20260428112747.png]]
	- only one mtype per model
	- must be defined globally 
- arrays:
	![[Pasted image 20260428112828.png]]

#### Basic Data Types
- Ranges:
	![[Pasted image 20260428112859.png]]
- Default initial values false and 0
- strictly bounded range of possible values
	- avoid state space explosion
	- automatic truncation if values lies outside the domain

#### Data Structures
- Record structures:
	![[Pasted image 20260428113033.png]]
- Multi-dimensional arrays:
	![[Pasted image 20260428113052.png]]
	- matrix elements references using $a[i].el[j]$

#### Expressions 
- Arithmetic:
	![[Pasted image 20260428113159.png]]
- Comparison:
	![[Pasted image 20260428113210.png]]
- Boolean:
	![[Pasted image 20260428113221.png]]
- Channel:
	![[Pasted image 20260428113234.png]]

#### Simple Promela Model
- One global variable 
- Two process type definitions (proctype keyword) 
- init process (started initially)
- run statement used to start other processes
	![[Pasted image 20260428113343.png]]

#### Promela Processes
- Can be started:
	- dynamically, using the run statement 
	- initially, if marked active, or if the init process 
- Concurrent execution of processes 
	- actions of running processes are interleaved
		- one exception: communication through synchronous channels
	- basic statements (e.g. assignments) are atomic
- non-determinism (several actions possible):
	- simulation mode: choice is made non-deterministically 
	- verification mode: all possible executions are explored

- Process type definition:
	![[Pasted image 20260428113640.png]]
	- Only basic data types as parameters (no arrays/proctypes)
- process instantiation:
	![[Pasted image 20260428113735.png]]
- special process init: started initially
- each running process has a unique identifier, _ pid  
	- non-negative integer assigned in order of creation

#### Promela Models and Transition Systems
- Each Promela model describes a transition system:
	- states: capture all current information in the model
		- current process counter for each active process
		- current values of local and global variables
		- current contents of active channels
	- transitions:
		- correspond to atomic statement executions 
- paths through the transition system correspond to possible runs of the model
- trace: sequence of states during a particular run
	![[Pasted image 20260428114152.png]]

#### A simple Promela Model
- ![[Pasted image 20260428114645.png]]

#### Message Channels
- Used to model (buffered) data exchange between processes
- Declaration:
	![[Pasted image 20260428114805.png]]
	- can store up to 10 messages,
	- each message consists of two fields, of type int and bool respectively 
- sending a message along a channel
	![[Pasted image 20260428114850.png]]
	- wait until c not full, then send exp1, exp2 along c
	- must send exactly as many message fields as declared, of the right type

#### Working with Channels 
- receiving a message on a channel:
	![[Pasted image 20260428115035.png]]
	- wait until c is not empty, then receive values in var1, var2
	- must receive exactly as many message fields as declared
- Channels have FIFO order:
	![[Pasted image 20260428115116.png]]

#### Asynchronous versus Synchronous Communication
- Asynchronous communication:
	![[Pasted image 20260428115154.png]]
	- where N is a positive constant 
- synchronous communication - via channels of size 0:
	![[Pasted image 20260428115227.png]]
	- Handshake between two processes
		![[Pasted image 20260428115251.png]]

#### Synchronous Communication Example
- Global Channel glob
- local channel loc
	- initially only visible to A
	- also available to B after the fist handshake 
	- only available while A active
	![[Pasted image 20260428115440.png]]

#### Working With channels 
- Sorted send !! and "random" receive ?? also exist, can be combined with normal send/receive
- predefined functions:
	- len(...), empty(...), nempty(...), full(...), nfull(...)
	- len(c) gives number of messages currently stored by c 
- can inspect the first message on a channel without removing it:
	- $c?[msg]$
- it is true precisely when the statement c?msg is executable, but has no effect on c or msg

#### Statements and Executability 
- Assignments: 
	- rhs must be side-effect free
		![[Pasted image 20260428115902.png]]
- null statement: skip
- run statements:
	- run process_id(param_values)
- above statements are always executable
- conditions:
	- any boolean expression is a condition
	- blocks until the condition is true
		- a == b
	- similar but not equivalent to:
		- while (a!=b) skip
- guarded statements:
	- have the general form: guard -> statement 
	- guard is usually a condition (boolean expression), but can be any statement: "->" is equivalent to ";" 
	- not atomic:
		- (turn == 1) -> turn = 0
			- blocks turn == 1, then becomes executable
- send(!) and receive (?)
- if ch has positive length
	- ch!exp executable if ch is not full
	- ch?var executable if ch is not empty
- if ch has length 0:
	- ch!exp executable if there exists matching ch>var waiting to be executed somewhere else
- compound statements:
	- atomic sequences
	- case selection
	- repetition

#### Inference, Blocking
- If A finishes before B starts, B is blocked on the initial state.
- Inference between A, B leads to different final value for s.
	![[Pasted image 20260428120556.png]]

#### Atomic Sequences, Blocking 
- atomic keyword can be used to make several steps count as single (atomic) step
- can be used to cut down level of interference/non-determinism 
- must be used with care
- the result of using atomic is that either A or B will block
	![[Pasted image 20260428120839.png]]

#### Atomic Sequences and Executability 
- Atomic chain broken by unexecutable statements
	![[Pasted image 20260428120923.png]]
	- Control relinquished after turn == 0
	- once turn == 1 becomes executable, control can non-deterministically return to the process

#### Control Flow: Case selection
- exactly one option is executed 
- only an executable statement can be executed
- if there is a choice, an option is chosen non-deterministically
- if there is no choice, process blocks
- else guard (if present) only executable if no other option is executable
	![[Pasted image 20260428121146.png]]

- Non-deterministic branching:
	![[Pasted image 20260428121218.png]]
	![[Pasted image 20260428121226.png]]
- Can be used to model program input

#### Control Flow: repetition
- Extension to case selection 
	![[Pasted image 20260428121323.png]]
- after each option, repeat the execution 
- termination via break statement, e.g.
	![[Pasted image 20260428121341.png]]
- else guard works as for case selection

#### Example
- Can block on i == 10
	![[Pasted image 20260428121447.png]]
- else branch avoids blocking 
	![[Pasted image 20260428121515.png]]

#### Examples:
- if (cond) then S1 else S2 equivalent to 
	![[Pasted image 20260428121604.png]]
- if (cond) then S1 equivalent to 
	![[Pasted image 20260428121622.png]]
- for (i=0, i<n , i++) S1 equivalent to
	![[Pasted image 20260428121643.png]]

#### Alternating bit protocol 
- The sender:
	![[Pasted image 20260428121751.png]]
- else branch prevents blocking on recvbit == sendbit
- else branch should not be reached if protocol was correct
- The receiver:
	![[Pasted image 20260428121902.png]]
- Sender and Receiver do not account for possibility of message loss
- Modelling Message Loss:
	![[Pasted image 20260428121941.png]]
- Daemon process "steals" messages
- _ acts as a write-only variable
- Sender and/or Receiver must be able to recover from message loss, otherwise protocol will deadlock

#### Timeout
- Predefined global variable timeout becomes true when there are no executable statements in any of the currently running processes
- so timeout models global timeout 
- timeout can be used to prevent deadlock in the model
	- but use of timeout should be consistent with the actual system

#### ABP 
- Improved sender:
	![[Pasted image 20260428122217.png]]
- easier to model message loss recovery in the sender
- Receiver model can stay unchanged 
- Improved receiver:
	![[Pasted image 20260428122322.png]]
- Receiver should only accept a message the first time it is received 

#### ABP Correctness properties
- Safety properties:
	- absence of deadlock 
- liveness properties:
	- progress + correctness
	- every message sent by S is received at least once and accepted at most once by R 
	- To check this we need to model the data being sent



# References