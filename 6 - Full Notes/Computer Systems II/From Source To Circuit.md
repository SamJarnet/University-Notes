2026-04-04 11:02

Status:

Tags: [[Computer Systems II]]


# From Source To Circuit

#### Source Code to Memory
- Why is it useful?
	- Important to understand C 
	- Useful to interpret error messages

#### Source Coder -> Compiler -> Executable
- Compilation 
	- Compiler executes on host architecture that is also the target for its output
- Cross-Compilation 
	- Target architecture is different from compiler host
	- We are doing cross compilation when we compile the c code for our PICO 2 W on our computer
- Compiler can optimise 
	- rearrange things 
- Harder to get good error messages  
	- You have to find the issue in the source code which isn't a straightforward mapping as stuff may have been rearranged to optimise 

#### Cross Compilation 
- Used when compilation on target is impossible or impractical
- Or First compilation on new hardware 
- Or Low-Capability target.
	- E.g. our PICO has hardly any memory 

#### Cross-Compilation Challenge
- The architecture of the host and target may be very different 
	- Memory architecture, e.g. von neuman or harvard (same memory for program and data vs separate) C is only designed for Von Neuman.
		- Advantage of Harvard .
			- no bottleneck as could fetch both program and data at same time, hard to get the CPU to execute data as its in a different memory so attacks are difficult
		- Why don't we use flash memory for everything?
			- It wears out so can't write too often
			- Fast for reading but slow for writing 
				- Would have to erase 512 bits and then rewrite them to change something in that block if writing a single bit
	- Word Size, e.g. 64-bit vs 8-bit
	- Byte order    endianness (order of which the bytes within a word data type are transmitted over a data communication medium)

#### Build Process
![[Pasted image 20260404112336.png]]
- These are cross-compiler, and also cross-linker and cross-assembler 
- The pre-processor is like a small language, in C its the stuff with a hashtag in-front like $\#INCLUDE$ which just reads a file and puts it in that place. Or define labels and replace them.
- Have to account for pre-processor in the error message as could be 200 lines of preprocessor and the error is after that but the compiler doesnt know your source code.
- Compiler has many stages like the lexer, parser and maybe intermediate code, outputs assembly code.
- Unlikely to get an assembler error, could get a pre-processor error like INCLUDE but the file doesn't exist
- Output of the linker depends.
	- For our PICO we have tools to load this into the PICO, for us that is a bootloader 
	- Could be a USB port

#### Build Process: Errors and Options
- Interpreting error messages
- Considering configuration options 
- We can steer the build process using:
	- Compiler Optimisation
		- Optimise for lower amounts of memory or higher speed
	- Compiler Warnings
		- How strict
	- Selection of libraries (paths and variants)
- Microcontroller might have some debug pins but if you need those pins as you have limited pins, its not good enough to just label it as a debug interface you have to do a specific sequence. e.g. write to the same port, the same bit twice within four instructions 
- Could use watchdog timers to turn them off but that also requires specific sequences with specific timings, and if your compiler is over-optimising it could break those timings
- Library may not have all functions as uses lots of memory like floating point printing with printf, would have to specifically tell compiler you want floating point for printf 

#### Build Process: Intermediate Files
- ![[Pasted image 20260404114505.png]]
- We are interested in the final link file, if nothing went wrong we will get a loadable file which is a standard binary format which can be processed further to extract the exact sort of memory layout, which can be written to memory
- If there is a problem somewhere we can get hold of the intermediate files, this shouldn't happen.

#### Linker Output: .elf object file
- Object File Types
	- Relocatable (.o) 
	- Executable (a.out/exe)
	- Shared object (.so/dll)
- ELF -> Executable and Linkable format
- Platform independent binary interface for object files
- Contains layout information and sections 

#### Sections 
 -  Memory segments laid out with virtual addresses.
	 ![[Pasted image 20260404115408.png|658]]
- There are 24 section types defined in ELF, but the ones above are sufficient for us.
- The instructions are all the commands that get fetched by the CPU to be executed, would be written to flash memory
- Read-only data is written to flash memory, don't care about speed as its persistent 
- Data segment is the initialised global variables, cant put in flash as we may want to write so its starts in flash and is moved to memory by the compiler when the program starts
- Uninitialised global variables are in RAM and are zeroed out, in C only for global variables and static variables are zeroed when not initialised
- Any local variable in a function which is on the function stack is not zeroed out. Programmer may not want variables to be 0 by defualt 
- If you want to know how full the stack is you need to know where it is in memory, in C you could create a local variable like integer x and then get hold of the address off that variable and that's where the top of the stack is, important that its not initialised.
	![[Pasted image 20260404120423.png]]

#### Use of the ELF sections
- 
# References