2026-04-28 19:45

Status:

Tags: [[Programming Language Concepts]]


# Coroutines

#### Subroutines as tasks
- Subroutines:
	- Control flow jumps to a named part of the program, executes all of the instructions in the named block and then returns back to the point of the subroutine call.
- One way of viewing execution of a subroutine is by imagining two tasks with their own control:
	- one task executes the main flow
	- a subroutine is called and then this main task is suspended
	- the subroutine task then takes over until it completes
	- control is then yielded back to the main task
- The main call blocks until the subroutine completes 
	![[Pasted image 20260428202339.png]]

#### Coroutines 
- We can generalise this idea then
- Imagine that calling routines simply as an instruction to suspend the current task and wait until resumed 
- rather than a single call out and single resume, this could happen multiple times and between many tasks 
- The execution state would need to be stored and reinstated each time the task resumed 
- This is the concept of coroutines 
- Coroutines don't wait until calls to other coroutines have been "completed" this is something like a non-blocking call
	![[Pasted image 20260428202644.png]]

#### Coroutines vs Threads
- This is not just threading, coroutines are not typically implemented using new threads
	- They can be single-threaded or they can make use of thread pools to re-use existing threads
	- They are lightweight as there are no system calls, no blocking, no mutexes and critical sections needed.
- Coroutines provide concurrency but not parallelism whereas threading can provide both
- Coroutines are designed to provide the benefits of programming in a cooperative multi-tasking style. Coroutines know exactly the control points where they will yield the processor 
- Threads are designed for preemptive multi-tasking - threaded code does not know when it will be interrupted and yield the processor 
	- It is this aspect of preemptive multi-tasking that makes it hard to ensure that code is correct. 
	- With cooperative multi-tasking ensuring that code is correct is much easier because of the predictable context switches

#### Example Using Coroutines 
- Kotlin Example
	![[Pasted image 20260428203147.png]]
- Another example:
	![[Pasted image 20260428203316.png]]

#### Kotlin Coroutines 
- Modern implementation 
- Built using coroutine builders (like launch and runBlocking) that accept a code block representing the task - they are identified using job references
	- jobs can be cancelled or combined using a job function
- Have a coroutine start mode that determines initial scheduling 
	- DEFAULT mode is immediate scheduling
	- LAZE mode starts the coroutine only when called
	- ATOMIC mode is as DEFAULT but is not cancellable before starting
	- UNDISPATCHED mode immediately runs until the coroutine is first suspended 
- Built using a coroutine context that stores information about schedules and allows coroutines to be arranged and dispatched hierarchically 
- have a notion of scope associated with them - this determines the lifetime of the task and how long the coroutine will run for. Globally scoped coroutines run as long as the main application thread is alive.

#### Unity (C#) Coroutines 
- Another good example of coroutines can be found in game development
- Every "frame", all of the game logic executes 
- What happens if this logic takes "too long" to process, or needs to be processed across multiple frames?
	- Lag stuttering freezing
	
	![[Pasted image 20260428204100.png]]
- Use a coroutine:
	![[Pasted image 20260428204141.png]]
	![[Pasted image 20260428204146.png]]

#### Goroutines 
- Coroutines in Go, more like lightweight threading
	- They are implemented using thread pools and run in parallel
	- use channels to coordinate their behaviour rather than using yield

# References