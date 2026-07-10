2026-04-06 12:15

Status:

Tags: [[Computer Systems II]]


# Memory Mapped IO

![[Pasted image 20260406121602.png]]

#### How is Software connected to Hardware
- Control Registers 



#### Control Registers
- Sets of flip flops which are not only connected for reading and writing: 
	- their inputs or outputs are wired to other circuits 
	![[Pasted image 20260406121730.png]]
- We don't typically have dynamic memory in micro-controllers 
- Must go through, measure voltage of leaking capacitors before its indistinguishable from a 1 or a 0 and recharge them
	- This interferes with accessing memory and slows it
- For each bit you need a small capacitor, very dense memory
- Some micro-controllers have registers themselves mapped into the memory addresses , but for some you have for a memory register for each normal CPU register 

#### How does the CPU interact with the control registers?
- I/O instructions 
	- Instruction set of processor has special I/O commands
		- So you don't accidentally overwrite a memory cell and cause a physical effect e.g. bomb (a bug in your program could cause that to happen so these are used instead)
	- I/O commands control I/O port registers
	- Pros:
		-  Hardware access is clearly separated from memory
		- Harder for bugs to accidentally trigger device operations 
		- Instructions may be shorter (port numbers may be smaller)
	- Cons:
		- Require special instructions in the instruction set 
		- Programmers must remember addition I/O commands
		- Compilers and architectures become more complex
- Memory Mapped I/O 
	- I/O registers have addresses in reserved memory space 
	- Memory Access
	- Pros:
		- Programmers don't have to remember what the I/O instructions are if they are writing assembly level stuff
		- You don't need extra instructions in your instruction set (now reduced opcode size is allowed -> less memory fetches?) 
	- Cons:
		- Instruction must contain large memory addresses
		- Instructions become longer 
- In some CPUs a mix of both methods are used

- CPU can educe instructions size by using registers instead of fully memory addresses since registers only require a few bits to encode 
	- Or use base(register) + offset addressing, where a register stores a large memory address and the instruction only contains a small offset
	- These methods reduce instruction length but limit the range of directly addressable memory. 
	- An even simpler design is a stack architecture, where operations automatically use the top values of a stack, so instructions do not need to specify operands. 


#### Special Instructions vs. Memory mapping summary
- Size of the address space
	- Not a concern now as its huge now 
- Convenience of space 
	- Different addressing modes 
- Size of the instructions set
	- Instruction bits are precious 
- Cache complications!
	- Input registers will change without instructions from the CPU

#### AT90USB1286: Address Spaces
- ![[Pasted image 20260406141236.png]]
-  C languages assumes Von Neumann, we can workaround with the intended address space is indicated to the linker by a specific big offset 
- AVR controllers use Harvard architecture with seperate Flash, SRAM and EEPROM memories.
	- Flash stores programs, SRAM stores variables, and EEPROM stores persistent data.
	- The compiler uses special offsets and instructions to access the different memory types while making the appear unified to the programmer.

#### AT90USB1286: Data Memory Map
- ![[Pasted image 20260406141745.png]]
- All hardware modules on the micro-controller are configured by writing to I/O registers
- All communication to and most communication from these modules are facilitated by reading and writing I/O registers.
- Even general purpose registers are mapped into memory address space. 
- The memory map places CPU registers, I/O registers, and RAM in the data memory space. I/O registers are split into normal and extended groups because short instructions can only address a limited number of registers. Hardware modules like timers, ADCs, and GPIO are configured by reading and writing bits in these I/O registers.  

#### GPIO Pins
- ![[Pasted image 20260406151327.png]]
- For an 8-bit port (e.g. PORTF), there are three registers mapped to memory:
	- DDRF (Data Direction Register)  - Decides if each pin is input or output 
	- PORTF (Data Register ) - Writes the output value (HIGH/LOW) 
	- PINF (Input Register) - Reads the current input value 
- Each bit corresponds to one physical pin
	- E.g:
		- DDRF bit = 0 → pin is INPUT  
		- DDRF bit = 1 → pin is OUTPUT

- All DDRF bits start at 0, meaning: 
	- All pins start as inputs 
- Reason:
	- If pins started as outputs, they might immediately drive external hardware, possibly causing short circuits or unintended actions (bomb) when the device powers on.
- Inputs are high-impedance and safe

- If a pin is configured as output 
	- PORTF bit = 1 → output HIGH
	- PORTF bit = 0 → output LOW
- If a pin is configured as input:
	- Read PINF bit → reads voltage level on the pin 
- There is a special feature :
	  Writing to PINF can toggle an output pin, allowing a single atomic instruction to flip a pin's state

- Inputs cannot be left floating, because they can pick up noise or random signals. 
	- So micro-controllers include internal pull-up resistors.
	- Typical circuit:
		- Vcc
		   |
		[Pull-up resistor]
	 	   |
	     Pin ---- switch ---- GND

	- Behaviour:
		- Switch state: Not Pressed:
			- HIGH (due to pull-up resistor)
		- Pressed: 
			- LOW (connected to ground)

- If the pull up resistor is too small
	- Large current flows when switch is pressed
	- wastes power
- If it is too large
	- Input becomes susceptible to noise 
- Typical value:
	- ≈ 40kΩ – 50kΩ
- This balances power consumption and noise immunity 
- We can access those types of registers in the header files.

#### Manipulating Register Bits
- ![[Pasted image 20260406153549.png]]
- Hardware registers are bit vectors, and C uses bitwise operations to modify individual bits safely. The `_BV(x)` macro creates a bit mask `(1 << x)`, allowing bits to be set using OR (`|`)or cleared using AND with NOT (`& ~`). Fixed-width types like `uint8_t` match the 8-bit registers used in microcontrollers.
# References