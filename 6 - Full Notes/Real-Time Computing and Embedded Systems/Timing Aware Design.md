2026-10-26 16:51

Status:

Tags: [[Real-Time Computing and Embedded Systems]]


# Timing Aware Design

#### Broader Design
- Design Decisions
	- What kind of decisions does one face when designing real-time systems?
- System Architecture 
	- Depicts the overall structure of the system, including both hardware and software
- Complexity in System Stacks
	- Stack complexity varies:
		- with or without device drivers
		- with or without an operating system
		- with or without middleware
			![[Pasted image 20261026165650.png]]
- Table: 
	![[Pasted image 20261026165735.png]]

#### Task Level Design
- What is a task?
	- A task is a schedulable unit, used as an abstract representation of a thread or even an application (as in many flight-control systems and similar domains)
	- A task represents a sequence of executions over time and may encapsulate one or more functionalities
	- In literature task $\approx$ thread and the two are often used interchangeably
- Convention in this module:
	- task - abstract design entity, particularly useful for scheduling and timing reasoning
	- thread - implementation of one or more functionalities

#### Functionalities Carried by Tasks
- Focus on cyber-physical systems
- "Envionmental Control" 
	- Continuously actuate the environment based on its current state
	- Typically subject to periodicity requirements 
- "Observe and react"
	- Monitor the environment, detect conditions of interest and trigger actions (react)
	- Typically subject to response-time (event-latency) requirements; often realised by periodic polling or event-driven/sporadic tasks
- Both can be designed using the same pattern, as a single task or with multiple tasks
	![[Pasted image 20261026170531.png]]

#### Decomposing Functions into tasks
- Separate functionalities 
	- A single task for many functionalities is rarely a good solution
		- Running all functions in one task at the rate dictated by the strictest timing requirement is often not possible (feasible)
		- Even when feasible, it wastes resources (CPU/energy) and reduces analysability
			![[Pasted image 20261026170739.png]]

- Sensor Access Strategy
	- When can multiple tasks use the same sensor?
		- If reads are quick and bounded (short, non-blocking I/O) and protected by brief mutual exclusion, tasks can share the driver.
		- If reads are slow, blocking, or complex, create a dedicated acquisition task that samples at a defined rate and publishes data (queue/mailbox/ring buffer) to other tasks.
			![[Pasted image 20261026171139.png]]

- Handle Common Computations Once
	- If activities need the same computed data
		- Compute it in a dedicated producer task and share the result
		- This avoids duplicated work, keeps one source of truth and simplifies maintenence and timing analysis.
			![[Pasted image 20261026171245.png]]

- Actuation strategy
	- When can multiple tasks write the same actuator directly?
		- Writes are quick and bounded (no long blocking)
		- Brief mutual exclusion suffices
	- When to add a dedicated actuator task (arbiter/mixer)?
		- Writes are slow/complex
		- Functionalities may conflict (e.g. cruise vs emergency brake)
			![[Pasted image 20261026171444.png]]

#### Periods
- A task's period determines how frequently it is invoked
- For a response-time requirement of $t$, the task period must be $\leq t/2$ to guarantee within $t$ (Shannon-Nyquist theorem)
- Multiple tasks:
	- Individual periods $\leq t/2$ are not sufficient to guarantee the overall response time; task periods must be coordinated, e.g. using equal or harmonic periods