2026-04-29 17:05

Status:

Tags: [[Computer Systems II]]


# Interrupt Handling

#### LED user interface
- pins are precious in small devices, an LED is a luxury and often as good as it gets for an embedded UI 
	- How many different states can you clearly indicate with a single one colour LED?
		- On off - 2
		- Blinking  - slow fast heartbeat fade in out - 4ish
	- What could you do with it?
		- Connect it to an app to read different graphs based of light level 

#### Basic I/O Methods
- Programmed I/O (Polling)
	- CPU sits in a tight loop (high CPU usage doing nothing like a while loop with nothing in it) until input is available or output can be accessed
	- Occupies CPU ("busy waiting")
	- Very fast reaction possible
	- could dedicate a whole core to do this 
		- maybe you want to measure something where speed matters like time of flight in radio signals on nanosecond scales
- Interrupt-driven I/O 
	- Hardware signal can change program flow
		- If something important happens on the outside, it can be indicated to your program by just moving the program to another part of the code
		- Harder to debug such systems and is harder to reason as outside event can change order of stuff
	- CPU can do other work (or sleep) unless I/O is possible
		- In earlier times if the CPU had nothing to do would run an idle task (do nothing) now we power down (sleep) 
		- you can make a microcontroller sleep so deep that the battery power consumption is almost the same as if you (micro amp level)
- Other I/O methods like Direct Memory Access (DMA) or dedicated I/O computers (e.g. a graphics card) use interrupts to communicate with the CPU

#### Program Flow 
- ![[Pasted image 20260429173126.png]]
- Most embedded systems cannot terminate, as on a computer it goes back to other things like the operating systems, but many embedded systems don't have an operating system. There is nothing it can terminate to.
- In the initialisation stage of the program flow you set all the registers, registers configure the hardware which tells you Memory mapping of registers, how to configure your timers, your communication or on the PICO the blink program. We have to configure the LED pin is an output pin from the GPIO pins.
- Can't get out of the loop in the main loop
- If you have an interrupt service routine, some sort of extra code that we can jump to and return to. Not readable in the code, happens through outside events
	- Whenever we reason about our program, keep in mind that that thing could jump somewhere else
	- If you have many ISRs debugging can get difficult

#### Interrupts 
- The solution to overcome the inefficiency of programmed I/O is a possibility to interrupt the CPU when I/O devices are ready to receive or deliver data.
	- I/O streams come at different rates, keyboard vs network different number of bytes per second
- The CPU needs to be able to continue where it was interrupted after the interrupt has been dealt with.
- The state of the interrupted process needs to be preserved
- Exception:
	- if interrupt should abort execution because of an irrecoverable fault (self destruct included)
	![[Pasted image 20260429173736.png]]


#### Precise Interrupt 
- State of program counter is preserved 
- Everything before PC has been fully executed
- Nothing beyond the PC has been started
- Execution state of instruction at the PC is known
- This can all get tricky if introducing pipelines, simple in simple CPUs

#### What happens when an interrupt arrives?
- Processor completes current instruction 
	- If you have instructions which are multiple instruction cycles long, interrupts may take different lengths of reaction times
- Processor acknowledges interrupt 
- Hardware saves some state:
	- Program counter 
	- Process status word (state of CPU)
		- for example contains flags about last instruction of the CPU causes a zero result 
- PC register is loaded with value from interrupt vector table
	- Multiple ways where it can jump as usually has multiple interrupt sources
	- usually has an interrupt vector table that's a part of the memory, all the address are written in where to jump if a certain interrupt happens and an address for where to jump to after reset (usually stored at low addresses of program memory) usually where the memory mapped IO addresses are as well. can be moved around on some machines in initialisation phase to gain a specific behaviour
- Control now handed to software

- Software disables interrupts
	- normally default settings of compiler will do this for you 
- Saves additional state
	- Registers -> Stack
	- incase you want to use registers in your ISR
	- You could if you have extra registers flip to a new register page which can be flipped back later
- May re enable interrupts 
	- Easier if not enabled
- Services the interrupt -> ISR
- Restore state (software)
- enable interrupts
- hardware: restores PSW and PC

#### Interrupt Service Routines
- Procedure that is executed when the interrupt occurs and that handles the interrupt 
- Two important rules:
	- Keep them fast:
		- avoid loops
		- avoid heavy instructions - no printf()
		- should not block -> no scanf()
		- you want to turn interrupts off, if you can speed them up you can turn the off faster
	- Keep them simple:
		- debugging ISRs is hard
		- especially if they can interrupt each other or themselves
- What happens if you interrupt code with a call to itself?
	- muddled up
- Sometimes use a smaller device as it is easier to get timing right over a bigger computer that is powerful enough to do real time

#### Why fast?
- If they are fast you can usually block all interrupts
- Life is simpler if you do not need to make your ISRs interruptable
- Stack size bounds are easier to establish
	- in embedded systems where we have limited memory we don't want to overrun the stack size. you want hard guarantees for how far your stack can maximally call
- No need for reentrant ISRs

#### Latency 
- How long does it take until the CPU can respond?
	- Not always the same amount for each ISRs 
	- if we have more registers to deal with it will take longer
	- may have to wait for the cycle to end first if you interrupt at the start it will take longer than if it interrupted at the end
	- if you turn of ISRs then that is a big impact on latency, maybe multiple instruction cycles long
- Is this delay deterministic?
	- Could be temperature dependent
	- you might be in another interrupt service routine 
	- if theres a timer you cannot handle that interrupt because the interrupts arrive at arbitrary time slots on your CPU clock, outside events that it can depend on
- Deterministic latency may be important in real-time applications: e.g., human operators and also control algorithms can adapt to deterministic latency, but struggle with random delays in control lines
- random delay is hard to debug

#### Maximal Latency
- We have latency due to hardware:
	- Current instruction is completed
	- hardware support to save state
- We also have latency due to software
	- software to safe state
	- maximum length of critical sections that disable interrupts 


#### Jitter
- Instructions cannot be interrupted 
	- DMA/CPU halting 
- Some instructions take more than one clock cycle
- The response time depends on the instruction executed when the interrupt arrives

#### How to keep ISRs fast and simple?
- Keep Interrupts off during the ISR
- Advantage:
	- No worries about stack depth
		- If we allow interrupts on interrupts they nest on the stack
	- No overhead for reentrant code 
- Disadvantage:
	- Latency
	- Lost interrupts
- ISR needs to be short/fast (always bounded)

- Move the data that needs processing to some buffer
- Set a global flag - volatile unit8_t 
- Return immediately 
- Check the flag in the main loop and do the work there

#### ISRs in C 
- C is good for embedded programming as it does not have dynamic memory built in which we often don't need. It doesn't have any I/O built in.
- The C language has no support for ISRs 
- Declaring ISRs is compiler specific
- One the PICO you can decide which interrupt types are more important to use than others, you can rank in priority. 
	- If a lower priority interrupt arrives, and you start saving the state of the CPU, then a higher priority interrupt arrives, it can take over that state saving and use it for itself.

- Instructions are not interrupted but
	- C statements are typically compiled into multiple CPU instructions
	- C statements can be interrupted
- So be aware your code could be interrupted at any moment so if step count is important, consider this 


## Event Driven Programming 

#### Program Flow 
- Anything that happens on the system is driven by interrupts 
	![[Pasted image 20260429194156.png]]
- It can be so extreme point on embedded systems, that the system is in an endless loop which does nothing and if an event from outside comes something happens. Endless loop sleeping for key FOB or something

#### Bicycle light
- Event driven systems can be just state machines 
	![[Pasted image 20260429202855.png]]

#### State machines
- Moor machine:
	- output depends only on state
- Forever loop
- Events drive transitions 

#### Internal and External events
- Internal e.g.
	- a timer overflow 
	- completion of ADC conversion
- External e.g.
	- analogue comparator exceeds threshold 
	- keyboard input
	- display refresh cycle

#### Events 
- Maximum arrival rate?
	- physical limit?
	- scheduler?
- Deadline for servicing?
	- cost if missed? -> hard to debug
		- make sure it is not overwhelmed by an unexpected rate of arrival of interrupts
	- what part is time sensitive?
- Longest time interrupts are disabled?
- Impact on other realtime code?

#### Interrupt Vectors & Interrupt Service Routine 
- Different interrupt sources <- Events
- Each is associated with an ISR:
	- ISR:
		- Procedure that is executed when the interrupt occurs and handles the interrupt
- There needs to be an ISR for every interrupt source that is enabled. For the processor to know where to branch to, there is a table at the start of the program memory with the interrupt vector the address of the ISR for each source
- You must individually enable interrupts on microcontrollers
	![[Pasted image 20260429211213.png]]
- Low addresses in persistent memory (flash memory) first would be reset vectors

#### ISR: Things to watch out for
- Variables
	- A variable that is used in the ISR and the main program needs to be declared volatile
		- this lets the compiler know that it can not be cached in a register
		- the value in the register can change without the compiler understanding that this can happen
			- it can change through an interrupt 
			- a timer 
	- Multi-byte variables
		- access atomically outside ISR
			- you might end up with two halves that don't fit together because an interrupt could have occurred in between reading 
			- if you want to make sure its atomic you turn off global interrupts 
- Registers 
	- Operations on registers that are used by the ISR and the main program need to be atomic
		- atomic means completes without interruption

#### Volatile is slow
- volatile will turn off all optimisation for this variable
- If a volatile variable is used a lot in the ISR, copy it to a local variable
	- this will work if the ISR does keep interrupts disabled

#### ISR Implementation 
- Register ISR
- Enable interrupt at device level
- Globally enable interrupts
# References