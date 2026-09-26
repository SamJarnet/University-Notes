2026-09-25 15:10

Status:

Tags: [[Real-Time Computing and Embedded Systems]]

# Embedded Architectures

#### RFID
- Are RFID cards CPUs?
	- Yes they are (pseudo-) Turing complete
- Are RFID labels CPUs?
	- Not (pseudo-) Turing complete

#### Embedded Computer System Definition
- Classical Definition:
	- A specialised computing system
		- Specialised: does one function well
	- Typical expectations:
		- Low power
		- Low cost
		- Physically small
		- One set of deadlines
		- Single CPU
		- Single chip
		- External peripherals
- Modern Definition
	- Typical expectations:
		- Power efficient
		- Cost efficient
		- Peripherals often on chip
		- Size determined by system
		- As many CPUs (GPUs, TPUs) as needed
		- As many chips as needed
	
	![[Pasted image 20260925151739.png]]

#### Temporal Requirements - Jitter
- The jitter $\Delta d$ can be seen as a uncertainty about the exact time-point the RT-entity was observed with respect to the action
	![[Pasted image 20260925152017.png]]

- Minimal Latency Jitter and Error-Detection Latency
	- Jitter should be much smalle rthan the total delay
		- E.g. Delay of milliseconds means delay jitter should be in microseconds
	- Hard real-time system are mostly safety-critical
		- Cannot afford long latency in detecting and processing an error
		- Typically sampling period is close to detection period
	
	![[Pasted image 20260925152444.png]]
- We are safe if d_computer + $\Delta$d_computer < d_sample
- Waiting usually means "wait at least this long"

#### Absolute vs Relative Deadlines
- Diagram to show deadlines being left behind, blue is computer time, white is the sleep time which is not always exactly the number we give it (Waiting usually means "wait at least this long")
	![[Pasted image 20260925152828.png]]
- This means the longer the system is running the further it gets left behind
	![[Pasted image 20260925152931.png]]
- This solves this issue as we sleep until a timepoint instead of sleeping for some time.

#### Jitter Example Operating System
- C++ example:
	![[Pasted image 20260925153223.png]]
- Target is 1ms
- Worst-Case error is 20ms
- On a low-spec laptop

- Most full operating systems have substantial jitter:
	- Cache misses
	- Out of order execution
	- Other user processes
	- Resource Locking
	- Scheduling quantum
- We an get very low average d_computer and d_sample
	- d_computer: 100 instructs takes ~30ns
	- d_sample: can schedule to within 1$\micro$s in unloaded system
- We also get very high worst-case d_computer and d_sample
	- d_computer: cache miss is 100ns
	- d_sample: scheduling quantum is 1-10ms

#### Jitter Example Embedded System
- Embedded example:
	![[Pasted image 20260925153910.png]]
- Target of 1ms
- Jitter of ~10$\micro$s
- Max error of 50$\micro$s

- Embedded systems can have very low jitter
	- SRAM rather than DRAM: every memory access takes the same time
	- Pinned cache lines: guarantee that certain cache lines stay hot
	- All processes controlled explicitly by user
	- Direct control over scheduling
- We an get very low worst case d_computer and d_sample
	- d_computer: 100 instructs takes ~3$\micro$s
	- d_sample: can schedule to within 10$\micro$s
- We also get very high average-case d_computer and d_sample
	- d_computer: 10-100x slower than normal CPU
	- d_sample: often limited to 10$\micro$s or more

#### Normal OS vs Embedded
- General purpose CPUs and OSs are designed for average case
	- Share resources according to current load
	- Maximise throughput according to current load
- Micro-controllers and embedded CPUs are designed for worst-case
	- Dedicate resources according to worst-case load
	- Minimise latency according to worst-case load
- "Slow" 100MHz embedded CPUs often better than "fast" 4GHz CPUs 
	- Tightly optimised OSs, or no OS
	- Precisely known work-load: 


# References