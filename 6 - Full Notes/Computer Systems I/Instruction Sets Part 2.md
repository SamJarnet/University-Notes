23-12-2024 22:03

Status:

Tags: [[Computer Systems I]] [[CPU]] [[Instruction Sets]]


# Instruction Sets Part 2


#### Recap:
•The instruction set lists all of the commands a processor can execute 
•Different instruction set architectures have different instruction sets, e.g. ARM and x86 
•Different microarchitectures may share an instruction set. e.g. Intel Core and AMD Ryzen
•Usually represented in Assembly Language 
•An instruction is made up of an Opcode and a set of result/operand references

#### Instruction Set Architecture Types:
- There are four main types:
	- Accumulator based
	- Stack based
	- Register-memory based
	- Register-register (load/store)
- And fifth:
	- Memory-memory
- Example: Perform 
	X = A + B 
	without destroying A or B

#### Accumulator ISA:
- X = A + B => 
			LOAD A 
			ADD B 
			STORE X
	- A is LOADed into the accumulator
	- B is ADDed directly from memory
		- Result is stored in the accumulator
	- Result can then be stored in memory 
- Accumulator is an input an output store
- Used by early computers

#### Stack based ISA - Operands:
- X = A + B => 
			PUSH A
			PUSH B
			ADD
			POP X
	- Both operands PUSHed onto the stack
	- Result POPped off the stack
- Needs a top-of-stack (TOS) pointer, or hardware stack
- Only the top of the stack is written to
- Memory transfer requires extra operations


#### Register-memory ISA:
- X = A + B = >
		LOAD R3, A
		ADD R1, R3, B
		STORE R1, X
- One input <= memory
- One input <= register
- Result => register 

#### Register-Register (Load/Store) ISA:
- X = A + B =>
		LOAD R3, A
		LOAD R2, B
		ADD R1, R3, R2
		STORE R1, X
	- Operands LOADed from memory to registers
	- ADD uses operands stored in registers
- Memory transfer requires extra operations


#### ISA Type Showdown:

![[Pasted image 20241223224646.png]]

#### Register-Memory or Register-Register?
- Register-Memory:
	- Simple code generation
	- Data can be accessed directly from memory
- BUT
	- Functionally commutative operations, non-commutative behaviour: 
		- source operand can be destroyed
	- Instructions require a variable number of cycles
		- Memory access can be slow and non-deterministic 

- Register-Register:
	- Fixed-size instructions
		- Simple encoding!
	- Simple code generation
	- (most) Instructions require a similar, known number cycles
	- Fast
- BUT
	- High instruction count


#### Memory-Memory:
- The fifth type of ISA
- Produces compact code
BUT
- Large variation in instruction size
- Large variation in execution time per instruction
- Memory access is the bottleneck
- Not used today


#### Are more registers good?
- To a point
- More registers:
	- may need longer instructions:
		- more bits to encode
	- means more to save on context switch
	- increases cost
	- increases complexity
	- Modern ISAs abstract physical registers behind architectural/logical registers

#### Architectural registers:
- The spec says:
	- x86-64 has 16 general purpose registers. 
- The implementation has: 
	- Zen 3 (AMD 7000) has 160 floating point registers and 192 integer registers. 
	- This is where register renaming comes in…

#### Which ISA is Best?
- It depends...
- But there is clearly a trade off:
	- Instruction complexity for code size

# References