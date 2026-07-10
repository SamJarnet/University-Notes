2026-04-30 15:37

Status:

Tags: [[Computer Systems II]]


# Multitasking and RIOS

#### Operating System
- Uniform interface
	- for users
	- for programs
- Management of resources
	- CPU time
	- Memory 
	- Access to devices
- Management of interactions
	- Desired:
		- networking, communication among users/processes
	- Undesired:
		- protection, security

#### OS: Multiprogramming
- Came about as CPUs were expensive, keep that CPU busy
- Multiple programs available for execution on CPU
- If one process needs to wait for I/O, the CPU can work on another process
	- increased throughput
	- increased CPU utilisation 
- Key issue: protection
	- Pseudo-parallelism 

#### Processes
- Processes/Task/Thread
	- an abstraction of a program in execution 
- A process has an entry in the process table that typically contains:
	- Instruction counter and stack pointer
	- Assigned address space
		- You can check whether that process says within that address space as part of protection
		- can program the memory management unit
			- specifies the range of addresses which have programs allocated to
			- causes an interrupt that brings control back to the OS if an address appears on the address path (segmentation fault) (also could specify read/write access)
	- Associated resources
	- State
	- (same as storing states for interrupts)
- Depending on the complexity of switching between and the level of isolation among process one also talks about tasks and threads

#### Process state
- Running -> currently using the CPU
	- in a single CPU device, it means nothing else has the CPU so the entire OS is just bits in memory and cannot do anything
- Read -> runnable but stopped to let another process run
	- in memory, all conditions for it to run are satisfied, but doesn't have the CPU
- Blocked -> unable to run until an external event happens 
	- waiting for something, could be for IO or are sleeping for some amount of time
- State transitions:
	![[Pasted image 20260430155900.png]]
- The scheduler will pick one from the ready set, and put it on the CPU runs it to completing and is gone or
- E.g. program tries to write, gets buffered and gets put in blocked set until some operation is completed

#### State Transitions of Processes
- Processes typically alternate bursts of computing with I/O requests. While waiting for IO they are blocked from CPU access
	- When does a process become ready?
		- They are just arriving, they arrive ready
		- The CPU takes a running process and the OS takes the CPU away from it and preempts it , putting it back into the ready set.
		- If a process was blocked for some time and the external event occurs e.g. a timer has expired
	- When does a process become blocked?
		- Waiting for IO
		- Synchronisation: waiting for another process to release lock or send a signal
		- Timers: a process might sleep for a set time
	- What happens if more than one process is blocked?
		- The OS puts them in separate lines (queues) based on what they're waiting for. They wait until their external event is triggered - unless they're deadlocked, then they are stuck forever.
	- What would happen if more than one process is ready?
		- You have to decide which one is picked

#### Scheduling 
- Scheduler
	- Decided which process from the set of ready processes will get the CPU next
- The requirements for the scheduler differ according to the nature of the processes and the computer system
	- Fairness
	- Response time
	- Throughput
	- Turnaround
	- CPU utilisation
	- Deadlines (hard/soft)
	- Predictability
	- Adherence to policy

#### Scheduling Algorithms
- According to what criteria can/should the scheduler select?
	- First-come first-served
		- easy to implement 
		- massive long running job can block a short job that arrives after it, severely hurting responsiveness
	- Shortest job first
		-  Shortest remaining time
		- both similar, prioritise the job that takes the least amount of time to finish
		- it is technically impossible to know exactly how long a job will run (halting problem)
		- relies on heuristics and statistics (past behaviour) to guess the length. great for predictable environments but hard for interactive systems where user input changes everything 
	- Round robin
		- quanta, preemptive, context switch
		- each process gets a small unit of CPU time (called quanta), if it doesn't finish it is preempted and put at the back of the line
		- Goldilocks problem with time quanta
			- too long, becomes like FCFS, responsiveness suffers 
			- too short, context switching overhead, saving and loading process states wastes too much CPU time
	- Priority scheduling
		- jobs are assigned a priority, the CPU takes highest priority ready job
		- issue, low priority jobs can suffer from starvation
	- Lottery scheduling
		- each process is given lottery tickets, the more important the job, the more tickets it gets. The OS picks a random number to decide who runs next
		- use case: excellent for soft real-time (like audio or video). if the sound is stuttering just give the audio process more tickets
		- it provides no guarantees, its based on probability, a process could be unlucky and miss every draw. it is never used in hard real time systems where a task must finish by a deadline
- fairness:
	- giving each process a reasonable share of the CPU
- Responsiveness 
	- Minimising the time between a user action and the systems reaction
- throughput: 
	- maximising the number of jobs completed per hour 
- overhead:
	- minimising wasted CPU time spent on context switching and cache misses

#### Context Switching
- Preemptive OS -> OS can switch among processes
- hardware interrupts or software interrupts (traps) are used to switch among processes
- Switch from user process to kernel process
- Switch from kernel process to user process
- Context switching requires CPU time - this time is wasted

#### Context Switching Cost
- Context switch overhead
	- Save/restore PC
	- save/restore stack registers
	- save/restore status register
	- save/restore general purpose registers
	- save/restore memory map
	- save/restore IO status
	- memory cache is invalidated
	- working set of pages is invalidated 

#### Round Robin 
- Every process gets a time slice and served in a fixed order
- Short quantum:
	- overhead of context switching is high
- Long quantum
	- long response time
	- good efficiency -> processes block for IO before quantum expires
- typically 20-50 ms

#### Scheduling Scenarios 
- Interactive Applications 
	- User on terminal 
	- Client on server
- Real time tasks
- Batch processing 

## Real Time Scheduling 

#### Constraints on Computation 
- Correct 
- Within deadline
	- soft real time systems e.g. multimedia
	- hard real time systems e.g. flight control
- within power budget

#### Real time Systems
- Interaction with physical environment 
	- vehicle, power plant, robot, assembly line
- Timing constraints
	- A correct reaction too late is not useful

## RIOS

#### Riverside/Irvine Operating System
- A minimalist but practical scheduler designed for embedded systems where RTOS might be overkill
	- Fixed priorities, tasks are decided at compile time 
	- preemptive multitasking, higher priority tasks can interrupt lower priority ones 
	- bounded stack usage, the system guarantees a limit on how much memory the stack consumes
	- simplicity, the core logic is approximately 20 lines of C code making it highly understandable 

#### Key technical concepts
- Tasks execute within the ISR:
	- the scheduler is called by a timer interrupt, and it calls the task functions directly from within that interrupt 
- Reentrant code: 
	- because the ISR can be interrupted by another instance of itself (nested interrupts) the code must be reentrant to prevent state corruption (it can be interrupted in the middle of its execution and safely entered again before its previous invocation has finished)
- Internal stack management:
	- RIOS maintains its own array runningTasks to keep track of which tasks are currently active
- No self-preemption: 
	- A task is blocked from interrupting itself; an instance of task A must complete before another instance of task A can start ( the scheduler is reentrant but the tasks are not allowed to self preempt)
- Library caution:
	- you must careful with non-reentrant library functions like printf() as they may use global variables that get corrupted during nested interrupts

#### Data structures and setup
- The system relies on a specific struct to manage task metadata
	![[Pasted image 20260430180713.png]]
- idle task: a special task (often assigned the value 255) that represents the CPU doing nothing
- priority: tasks are stored in an array; the lower the index in the array, the higher the priority (e.g. index 0 is the highest)

#### The scheduling loop
- The scheduler runs every time the interrupt triggers. It iterates through the tasks to find the highest priority "ready" task
- Logical conditions for running a task:
	- A task i will only run if:
	- It is ready: 
		![[Pasted image 20260430180945.png]]
	- It has priority: the task index i must be lower than the currently running task's index 
	- No self preemption: 
		![[Pasted image 20260430181028.png]]
	- the task is not already active

#### Task management and atomicity
- RIOS uses atomic blocks to manage the transition between the scheduler and the user tasks 
	- cli() (clear interrupts) disables global interrupts to perform critical updates to the task stack and running flags
	- sei() (set interrupts) enables global interrupts, allowing a higher priority task to preempt the current one 
- Execution flow:
	- Start task: inside a cli() block, mark the task as running and push it into the runningTasks stack
	- Run task: Call TickFct. This happens after sei(), so this task can be interrupted by higher-priority tasks
	- End task: Inside another cli() block, mark the task as not running and pop it off the stack

#### Stack Depth and Worst Case scenario 
- A critical advantage of RIOS is that the stack depth is bounded 
- The bound; The maximum number of stack frames is limited by the total number of tasks in the system
- Worst case condition: the maximum stack usage occurs if tasks are triggered in reverse order of priority
	- if the lowest priority task starts, followed by the second lowest etc, they will all end up nested on the stack
	- the total frames on the stack would be approximately 2 x N + 1 (where N is the number of tasks), accounting for the main program, scheduler calls, and the tasks themselves



# References