20-10-2024 22:06

Status:

Tags: [[Computer Systems I]] [[Registers]]


# Types of registers

#### User visible registers: 
- General purpose
- Data
- Address only (not common now)
- Condition codes in status register

###### Address only registers:
- Never store your data
	- Only stores address
	- e.g. Segment or address register
	- Point to somewhere in RAM
- Stack pointers are used to point to a block of RAM for storing intermediate/dynamic values

###### How many general purpose registers are needed?
- Typically about 16 (i7 and ARM)
- Fewer leads to more memory references
	- If code needs to free up, a register it has to copy its data to RAM
- But they take up processor silicon area

###### How big?
- int = 32 bit
- long int = 64 bit
- float = 32 bit
- double = 64 bit
- This is large enough to hold a full address:
	- 32 bits could address 4GB
	- more is needed for larger RAM but a scheme is used to split it into sections

###### Condition Code Registers:
- Sets of individual bits
	- e.g. result of lost operation was zero
- Can be read (implicitly) by programs
	- e.g. Jump if zero
- Can not (usually) be set by programs 

###### Status / FLAGS register: 
- A set of bits with separate meanings
	- Condition codes 
	- Sign of last result
	- Zero
	- Carry
	- Equal
	- Overflow
	- Interrupt enable/disable
	- Supervisor

###### Control Register:
- Instruction Decoding Register
- MAR
- MBR
- May have registers pointing to process control blocks or interrupt vectors

# References