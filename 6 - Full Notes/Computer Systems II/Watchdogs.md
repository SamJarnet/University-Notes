2026-05-05 16:10

Status:

Tags: [[Computer Systems II]]


# Watchdogs

#### What's the point of watchdogs?
- If there is a fault which we can recognise we want to recover from it.

#### Autonomous Fault Recovery
- Typical embedded systems need to operate continuously, but cannot rely on human supervision.
	- system not easily accessible 
		- implanted device
		- space probe
	- human supervision is too costly 
	- human supervision is too slow 
- Use a watchdog to supervise the system

#### Watchdog 
- Hardware counter with its own Clock => Timer
	- The PICO 2 W does not have its own clock it has one of the multiple clock blocks which are on the system.
- When timer runs out, system receives a hardware reset. "dog bites" 
	- can do an interrupt 
	- can choose level of reset, certain hardware or whole system
- Software in normal operation restarts the timer before it runs out "kick the dog"

#### Software Faults
- Endless loops 
- Interrupt flood 
- Deadlocks from multitasking  

#### Watchdogs on the RP2350
![[Pasted image 20260505162133.png]]


#### How do we use it?
- Using a feature of a microcontroller:
	- Read the relevant section in the datasheet
	- Look at the library support 

#### Code sample: Watchdog use
- ![[Pasted image 20260505162527.png]]
- ![[Pasted image 20260505162600.png]]
- We will first check whether we have rebooted by the watchdog
	- Make sure deadlines are still met
	- Maybe do an endless loop to avoid messing up 
- We can ask what caused the rest
- Flag for debugging

#### Power consumption 
- If the watchdog is enabled it will run in all sleep modes and always consume power. This may be the dominant power consumption in a deep sleep mode.
- The watchdog's oscillator is much slower than the typical main clock and requires therefore less power - it can be used to wake from sleep instead of a timer running off the main clock.

#### Protection
- It is important that a run-away program will not accidentally disable the watchdog timer before it times out.
	- The are typically (processor specific) protection methods
	- Might have to be careful about flags on the compiler because you have to do something in a certain timing
	- This means if you change optimisation settings on the compiler, the timing might not hold anymore 
- It is important that the watchdog timer is not accidentally disabling a system.
	- If the watchdog timer is not used always clear its enabling bits at the start of program initialisation 
	- Be careful of random bit flips turning things off or on in programs

#### Diagram
![[Pasted image 20260505165207.png]]

#### Software Reset
- Applications for the Watchdog timer:
	- Fault recovery
	- Low power oscillator 
		- wake up from sleep
		- timing not precise 
	- Clean software reset
		- Firmware update
			- bootloader
		- Enable watchdog
		- Enter endless loop
			- so nothing else can be touched or go wrong
		- Make sure all peripherals reset correctly too

#### Watchdogs differ from device to device
- Some watchdogs can only be enabled, but not disabled
- Some watchdogs allow an extra delay during the first time out period 
	- account for initialisation period
	- could create weird debugging situations
- Some watchdogs are disabled after a timeout
	- need to be enabled during initialisation 
- Watchdogs have different modes - know which node is active
	- might interrupt, might reset or both

#### Stuck tasks
- Time-outs should protect any task that waits for external events from locking up indefinitely 
	- maybe broken peripheral
- Watchdog can be the last defence or part of the timeout design
	- critical system?
	- cost critical?

#### Multitasking: monitor task
- Monitor task can watch over other tasks 
	- this is the only task allowed to restart the watchdog
- All tasks report their operation by acting on a global set of flags
	- e.g. clearing the flag when a task completes
	- could be a bit in a register, could be unreliable if the bit flips 
		- use a bit vector instead
		- or just more bits
		- these bits need to be positioned in a way that the system going crazy cant overwrite it 
- Monitor task only restart the watchdog if all tasks have reported success 

#### Multitasking: Time scales
- Often tasks run at very different time scales
	- A frequent high priority task may be critical
	- A less frequent task will report at a much lower frequency
- How can this be handled?
	- You can skip the check on certain tasks, e.g. check every tenth time

#### Event-driven tasks 
- Tasks may arrive at unpredictable intervals 
- How can the execution of such tasks be monitored with a watchdog?
	- 

#### Robust Monitoring 
- Assume that random bit-flips can happen 
- How can the task monitoring be hardened against not recognising faults?
	- monitoring has to be robust

#### What to do when the watchdog triggers?
- reset is often a good option 
	- start from a clean state
	- keep periphery in mind
- Try to make it known that there was a watchdog reset
	- Flash LED
	- log the event too EEPROM



# References