23-12-2024 20:44

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Instruction Sets

#### What is an Instruction Set?
- At a high level, an instruction set is a list of all the commands that a processor can execute
- Different instruction set architectures have different instruction sets e.g. ARM and x86
- Different microarchitectures may share an instruction set. e.g. Intel Core and AMD Ryzen

#### More detail:
- A term you will come across is "machine code"
- This is what is executed
- Binary
- Usually represented by assembly language
	- One line of assembly (typically) produces one machine instruction

#### Elements of an Instruction:
- Operation code (opcode)  -> do this 
- Source operand reference -> use this item of data
- result reference -> put the answer here 
- Next Instruction Reference -> when you have finished, do this... 

#### Fetch -Execute Cycle 
- Fetch: 
	- get the instruction from memory 
- Decode: 
	- Work out what the instruction is 
- Execute:
	- Run it. 
	- This may involve reading input data from memory.
- Store: 
	- Write the result back to memory

#### Instruction Types
- Data processing
- Data movement (read/write main memory, I/O) 
- Program flow control

#### ALU: Arithmetic Instructions 
- A set of mathematical operations: 
	- Add, Subtract, Multiply, Divide
- Could be (signed) Integer or Floating point 
- May include:
	- Absolute (|x|) 
	- Increment (x = x + 1, x++) 
	- Decrement (x = x – 1, x--) 
	- Negate (x = -x)

#### ALU: Shift and Rotate:
- Shifting bits around is important:
	- bit masks
	- unpacking data
	- Fast integer arithmetic
		- e.g. a bit shift is a very fast integer multiply or divide by two
- Rotating is useful for several tasks, including cryptography

#### ALU: Logical Instructions 
- Bitwise logic operations 
- Think logic gates…

#### Control Transfer Instructions:
- Control program flow:
	- Allow for conditional expressions
- Branch (may be conditional)/jump
	- e.g. branch to X if < 0
- Skip
	- Skip the next instruction (may be conditional)
- Subroutine
	- Call some other code, e.g. interrupt function, routine
- Loop
	- Think hardware-assisted for loop

#### Data Movement:
- Move data about inside the processor
- e.g. Load, Store, Exchange, Move, Set, Push, Pop
- Each instruction has a source and destination
- May have length, depending on instruction set

#### Input/Output:
- Getting data in and out of the CPU and memory.
	- i.e. writing to/reading from disk, network or maybe a peripheral like a GPU
- May be specific instructions
- May be done with data movement instructions
	- Known as memory-mapped I/O
	- Some of the address space points to device
- May be done by a seperate controller
	- DMA: Direct Memory Access
	- Much faster as the data doesn't go through the ALU


#### How many addresses per instruction?
- More addresses:
	- More complex (powerful?) instructions
	- More registers
	- Register-to-register operations are quicker
	- Few instructions per program
- Fewer addresses:
	- Less complex (powerful?) instructions
	- More instructions per program
	- Faster fetch/execution of instructions
- Compromise! Trade-off necessary...

#### RISC vs. CISC:
- CISC: Complex instructions that do a lot of work
	- Could take multiple clock cycles to execute
- RISC: Simpler instructions, but more of them to do the same work
	- Generally one clock cycle per instruction
	- Code is larger than CISC

#### Alignment:
- Memory is byte-addressed
- But organised in multi-word blocks
	- e.g. 32-bit, 64-bit 
- Native objects have fixed sizes and convenient padding/alignment
- User-defined objects can be of arbitrary size and alignment
- Reading miss-aligned data may need multiple memory reads and a shift


#### Endianness:
- How are bytes in a word ordered?
- How are bits in a byte ordered?
- No consistency or consensus
- Not a problem at higher levels of abstraction 
- Can be a problem if
	- you are working at a low level
	- communicating between systems that do it differently


#### Byte Ordering:
- Consider the 32 bit hex literal 0x12345678, stored byte aligned at 0x900
- Big endian stores the most significant byte in the lowest numerical address
- Little endian stores the least significant byte in the lowest numerical address


#### Endianness Pros and Cons:
- Field addresses are the same for both schemes
	- Endianness does not affect the order of the fields in a structure
- Big endian memory dumps are left to right
	- For Western readers, this may be easier to read
- Big endian machines store character strings and integers in the same order (MSB first)
- Big endian has to perform an extra operation (addition) when converting from a 32 to a 16 bit address

#### Bit ordering 
- "First" bit can be bit 0 or bit 1 (usually 0)
- Lowest bit number (0 or 1) can be assigned to the LSB (little endian) or MSB (big endian)
	- No consensus 
- The choice of big/little endian bit ordering in a byte is not always consistent with byte ordering in a multibyte scalar
- No consistency, even within a single machine
	- If you really need to know, write a test program
- Can be an issue for communications 
  
  
[[Instruction Sets Part 2]]
  
  
  
# References