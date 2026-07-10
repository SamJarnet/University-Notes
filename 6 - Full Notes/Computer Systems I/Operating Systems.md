03-10-2024 17:15

Status:

Tags: [[Data Management]]

# Operating System 1

#### Definition:
- Enables the computer hardware to communicate and operate with the software
- Manages access to CPU time, memory and storage
#### Key features:
- Multi-user
	- Allows for multiple users to use the same computer at the same time or at different times (e.g. your [[UNIX]] servers)
- Multi-processing
	- Supports and utilizes more than one computer processor. Can be tightly (high-end servers) or loosely coupled (cluster of computing nodes)
- Multi-tasking
	- Allows multiple software processes to run at the same time

#### Purpose:
- Concealing complexity by protecting users with UI:
	- Internet protocols
	- Compilers 
	- Device drivers
- A starting point for designing your own software
- The OS protects the programmer and user from the details of the hardware
- It provides an interface to the hardware, so that other programs can make effective use of the computer
- This works much better if the hardware provides support for the OS
- Operating systems and hardware have developed together

#### OS kernel services:
- Memory Management:
	- Allocate memory for programs
	- Manage virtual memory 
	- Protect against programming errors and malware
- Task management:
	- Launch processes (process = program + state of program)
	- Maintain process table: list of running processes
	- Carry out timeslicing and context switching 
	- Handle interrupts
	- Set program privilege levels
-  File management:
	- Respond to program requests to open, read, write and close files
	- Set and check permissions
	- Handle buffering
- Device management
	- Use device drivers to respond to program requests to open, read, write and close devices such as printers, cameras, displays or keyboard


#### Essential hardware features for an OS:
- Memory protection:
	- To protect the OS
	- To allow the OS to protect programs from each other
- Timer:
	- To prevent a job monopolising the system
- Privileged instructions:
	- Only executed by OS, e.g. I/O
- Interrupts:
	- Allow for relinquishing and regaining control

#### Scheduling:
- Making effective use of the processor
- Central facts:
	- Memory access is very slow compared with processor speed
	- I/O devices are extremely slow compared with the processor
	- Multiple tasks need to share the machine
	- A processor can only do one thing at a time
- While one task is waiting for an I/O device (or the user), another task should be able to use the processor

#### Processes and context-switching:
- A process is a running program
- A process includes (roughly):
	- Code
	- Data
	- Resources (e.g. file descriptors)
	- Current state: registers
- Context switching means that the state of a running process is saved, and another process given processor resources.

#### Process Control Block (PCB):
- Identifier
- State 
- Volatile environment
	- Program Counter
	- Memory pointers
	- Context data
- Priority
- I/O status
- Accounting information

#### Types of scheduling:
![[Pasted image 20241111120927.png]]

#### Memory management - Why?
- To make the user think there are an arbitrary number of processes running at the same time
- To make every process think it has infinite memory
	- Engineering interpretation of infinity:
	- Entire address space, 32 bit machine ~ 4 GByte
	- Entire address space, 64 bit machine ~ 16 EByte (Exa = $10^{18}$ ~ $2^{60}$)
- Virtual memory (VM) does just this

#### Swapping:
- The OS stores a queue of processes wanting to execute
	- Processes on the disk, queue in the kernel
- As space becomes available, the processes are loaded
- When a process finishes, it is removed
- A process may also be swapped out if it is stalled (for example, waiting for I/O)

#### Partitioning:
- Fixed size memory partitions
	- "Typical" usage implies a logarithmic distribution of partition sizes is best
	- Easy to administer
-  Variable size memory partitions
	- Memory is allocated as required
	- Fragmentation makes it harder to load incoming processes

  [[Operating Systems 2]]
  
  
  
# References