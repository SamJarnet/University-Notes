2026-04-17 16:01

Status:

Tags: [[Programming Language Concepts]]


# Concurrency

#### Concurrency vs Parallel Computing 
- What is parallel computing?
	- Multiple computations are created by dividing a task into smaller, independent pieces of work. These are then executed simultaneously.
	- Can be multi-core, symmetric multiprocessing, distributed, massively parallel.
- What is concurrency?
	- Several computations executing simultaneously, potentially interacting with each other - this is typically done on a single (multi-core) machine


#### First Principles 
- What is clear form the definition of concurrency is that in this computational model, the simultaneously executing tasks will interact. 
- We call each executing sequence of control a thread
- For threads to interact they must be able to synchronise
- This means that threads must be able to send signals to other thread and threads must be able to recognise when signals have been sent from other threads.
- This is the basis of all inter-thread communication however how the signals are sent, what information is sent with them and how the threads synchronise on signals varies greatly across systems.

#### Signal and Wait
- One paradigm of synchronisation is that of "signal and wait" 
- A thread that signals another thread sends its signal and then enters a waiting state so that it cannot be scheduled further until the signal is received.
- This is also called synchronous communication - threads that are communicating rendezvous at a given point in their execution. 
	![[Pasted image 20260417161353.png]]

#### Signal and Continue 
 - An alternative paradigm of synchronisation is that of "signal and continue" 
 - A thread that signals to other threads does not need to wait until signal is received. It may continue its execution immediately after signalling. 
 - This is also called asynchronous communication - threads that are sending do not need to rendezvous. Threads that are receiving signals do still need to rendezvous on a signal.
	![[Pasted image 20260417161613.png]]

#### Semantics First
- If we were to introduce concurrency support into a programming language, a reasonable way of starting would be to consider the semantics.
- We would need to choose the synchronisation mechanism and what operators the language will feature
- How do we write down a small step semantics for multiple threads?
- We could imagine a relation of the form:
	- $T_1,T_2 ... ,T_n \rightarrow T_1',T_2' ... , T_n$
- where each thread $T_i$ may execute in a single step
- Where is the interaction?

#### No Thread is an Island
 - The semantics of each individual thread cannot be considered in isolation. 
 - The semantics of each thread must consider the interactions it makes with the environment in which it executes.
 - This can be interactions with memory, with other threads etc.
 - The semantics of a thread could therefore be defined as a small step operational semantics where the relation also includes an indication of any interaction the thread makes as well as computation steps internal to the thread.
	 - $T \xrightarrow{action} T'$ 
	 - Here, "action" refers to whether the thread is sending a signal, receiving a signal or reducing without interacting.

#### Multiple Threads
- ![[Pasted image 20260417162220.png]]
- Where actions may synchronise - i.e. action-i-k and action-j-k may be complementary send a receive signal actions. 
- On action-i-k and action-j-k' may be write to memory and read memory actions. 

#### A Simple Concurrency Calculus 
- Just like the lambda calculus is a language used for the study of pure functions, we can define small calculi for studying concurrency.
- We use CCS, which distills the essence of concurrent threads of computation that may execute both independently and by communication with other threads.
- The semantics of the calculus is given in the style described above by operational semantics  with extra annotations indicating the kind of action being performed. 
- CCS is a type of Process Calculus 

#### Syntax of CCS
- Grammar of CCS:
	![[Pasted image 20260417163547.png]]
- nil is an inert process - it has terminated
- a!P sends a signal on a channel named 'a' and then continues execution as P
- a?P receives a signal on a channel named 'a' and then continues execution as P
- $\tau \,$ P takes an internal computation step
- P || P represents two concurrent processes, this models thread spawning also
- P \ a is a restriction operation - no communication on channel 'a' originating inside of P can be seen.
- X and rec X . P are used for recursive behaviour e.g. rec X . a! b? X is a process that repeatedly sends a signal on 'a' and receives a signal on 'b'.

#### Example CCS Process
- An example CCS process is given below;
	![[Pasted image 20260417164019.png]]
- Server thread P1 publishes an invitation to client threads P2 and P3 to respond on channel 'b'. The first to do so gets to interact with P1, the other is blocked.
- Client thread P2 or P3 calls channel 's' some number of times and calls 'z' to finish. Process P4, counts the number of signals sent on channel 'e'.

#### Variations of Synchronisation 
- The semantics of CCS are typically presented as synchronous communication
- The rule for communication looks like:
	![[Pasted image 20260417165334.png]]
- This says, if P is ready to send a signal on channel 'a' and Q is ready to receive a signal on channel 'a' then when both P and Q are executing in parallel then they may communicate to produce a computation step internal to P || Q 
- In this case, if P is ready to send a signal it must wait until there is a corresponding process Q to receive the signal
- This is also what is known as a handshake communication as it only involves a single sender and receiver 

#### Asynchrony in CCS
- we adjust the grammar to forbid any continuation of the process after a send signal.
- That is:
	![[Pasted image 20260417165634.png]]
- In this case, a communication would take the form e.g.
	- ![[Pasted image 20260417165701.png]]
- In this example, the leftmost process can receive a signal on channel 'a'. It then spawns a new thread that does nothing but send a signal on 'b' and can immediately proceed as P without waiting.
- The rightmost process may eventually receive the signal on channel 'b' if it receives a signal on 'c' first.

#### Broadcast Communication 
- Another common communication mechanism that one sees is that of broadcast (as opposed to handshake) communication
- In that model, a signal is sent to all concurrent processes that are ready to receive that signal, not just a single process. 
- The process calculus CSP - Communicating Sequential Processes uses this 
- This calculus is similar to CCS except for the broadcast communication and a denotationally presented semantics rather than the small step operational semantics of CCS

#### Non-Determinism 
- Running the whole system of the previous example has no determined behaviour 
- The number of signals ultimately sent on channel 'e' depends on whether P2 or P3 first responds to the initial signal 
- This choice is made by the OS scheduler in practice
- In this calculus, either interaction can be taken
- What is clear is that the semantics of a process does not take the form of a single sequence of labelled reductions 
	![[Pasted image 20260417171724.png]]
- Rather, the semantics of a process forms a tree of labelled reductions as choices are made in the overall system behaviour. 
- Versions of CCS sometimes also include an explicit choice operation - P + Q that means, behave like P or behave like Q next.

#### Complex Semantics 
- Therefore, when it comes to understanding a concurrent program, we must consider each of its threads and the semantics of each thread can be represented as a tree of behaviours.
- When considering whether an implementation of a particular thread meets its semantics we must have a means of considering:
	- the actual behaviour of a thread (as a tree of actions) and 
	- the specified semantics (as a tree of decisions)
- We need a way of comparing trees of actions 

# References