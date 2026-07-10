20-10-2024 21:36

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Registers

#### Definition:
- A register is a group of [[Flip-Flops]] that can store multiple bits
- Store the data being worked on in the CPUs
- Are the fastest types of storage
- Are made up of flip-flops

#### How are registers used?
- Flip-flops are limited because they can only store on bit
	- Most computers work with integers and single-precision floating-point numbers that are 32 or 64 bits long
- Commonly used as temporary storage in a processor
	-  They are faster and more local than main memory
	- More registers can help speed up complex calculations
- Few are needed to store current variables which need processing so values just keep growing with more arithmetic

#### Shift Register:
- Shifts its output once every clock cycle
- One application of shift registers is converting between "serial data" and "parallel data"
- Computers work with multiple bit quantities
	- ASCII is 8 bits
	- int, floats are 32 bit
- Sometimes receiving data serially (one bit at a time) is necessary (keyboard, mouse, USB, SATA...)

#### More on registers:
- Registers store data in the CPU
	- Used to supply values to the execution units
	- Used to store the results
- Registers are expensive
	- They occupy space on a chip - in the core
	- L1 and L2 cache are very fast RAM which act as a buffer to main DRAM
- There are many different [[Types of registers]]

#### Supervisor mode:
- Controlled by status register/flag
- Intel calls this "ring zero"
- Kernel mode  - allows privileged instructions to execute 
- Used by [[Operating Systems]]
- Not available to user programs

# References