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

#### Specialisation of embedded processors and OSs 
- General Purpose System:
	- OS:
		- Complex and general purpose
		- Set of tasks discovered at run-time
		- Tasks scheduled by CPU availability
	- Processor Architecture:
		- Optimised for performance
		- Extensive use of caching
	- Input/output & peripherals
		- Optimised for throughput
		- General purpose IO buses
		- Plug and play for any device
- Embedded System:
	- OS:
		- Minimal or non-existent
		- Set of tasks fixed at design time
		- Task scheduled by task deadline
	- Processor Architecutre:
		- Optimised for predictability
		- Limited use of caching
	- Input/Output & Peripherals
		- Optimised for latency
		- Multiple specialised buses
		- Hard-wired connections to devices

#### Embedded Computer System
- CPU:
	- Model of a simple CPU:
		![[Pasted image 20260929100705.png]]
		- About right for an in-order CPU
		- Way too simple for out-of-order
	- Instructions move through sequentially:
		- Fetched from the instruction memory
		- Calculations done in the ALU
		- Retired by writing back to registers or memory
	- So where is the jitter/unpredictability?

- More realistic CPU
	- Model:
		![[Pasted image 20260929101006.png]]
	- Data reads and writes serve two purposes
		- Data: reading and writing stack, heap, ...
		- IO: interacting with external devices
	- Data reads and writes are often cached
		- Memory is much slower than the CPU
		- Most data is reused, so cache it locally
	- Instruction fetches are often cached
		- We need to fetch an instruction every cycle
		- Most instruction are reused, so cache locally
	- We want to run parallel instructions
		- Need to schedule them at run-time
	- Many sources of jitter = noise distribution
		![[Pasted image 20260929101238.png]]
		- Some are independent 
		- Some are predictably correlated 
		- Some are unpredictably correlated
		- Many are very long tailed distributions
	- A good example is caching

#### Abstracted and Compacted Control Loop
- ![[Pasted image 20260929101519.png]]
- ![[Pasted image 20260929101532.png]]

#### Compact control loop with:
- Normal and Critical Actions:
	![[Pasted image 20260929101817.png]]
- Combined Action and Pinning:
	![[Pasted image 20260929101741.png]]
	- Must pin so that you don't get a cache miss
	- Don't overpin or theres no point in a cache

#### Caches are bad for jitter
- Caches are all about average case performance
	- They are extremely effective for that
	- They are used everywhere
- High performance processors have caches everywhere
	- Memory caches, Instruction caches (common in embedded too)
	- Decoded instruction caches
	- Branch prediction caches
- General purpose OSs add virtual memory
	- Virtual memory pages get mapped to physical pages
	- Any user memory access may require a disk read or page decompression
	- Processor also requires a cache of virtual->physical mappings

#### CPU to IO: Windows / x86 vs Arduino
- Windows/x86:
	- Hardware:
		- CPU -> PCI Express -> USB Hub -> USB -> UART
	- Software / APIs:
		- User-code -> Library -> Kernel-code -> USB Device driver -> PCIe Device Driver
	- All sources of jitter
- Arduino:
	- Hardware:
		- CPU -> UART
	- Software/APIs:
		- User-Code -> Library UART; or
		- User-code -> UART

#### What is IO?
- From a software POV: how does code access it?
- From a hardware POV: what is the physical transport?
- Transaction POV: when does IO begin and end?
- Abstraction: what is the conceptual model?

#### IO as a channel
- One of the most common IO abstractions is a channel or stream
	- Output: a channel that you can write a sequence of data into
	- Input: a channel that you can read a sequence of data from
- Examples of IO as a channel:
	- stdin/stdout: stdout, print ...
	- Files: model storage as a stream of bytes
	- TCP: a reliable channel that can transport data
	- Streaming buses: AXI streams or Avalon streams

#### IO as a mapping
 - Another common IO abstractions is a dictionary or mapping
	- Output: read the value associated with a key
	- Input: change a value associated with a key
- Examples of IO as a mapping:
	- RAM: key=address, value=word
	- Files: key=offset, value=byte
	- Directories: key=path, value=byte stream
	- Real-time DB: key=object id, value= latest measurement

#### IO at the CPU boundaries: channel or mapping?
- Embedded CPUs need to connect to multiple types of IO functions
	- Channels: audio data, pixel streams
	- Mappings: LEDs, switches, any sampling sensor
- Embedded CPUs have multiple types of underlying physical connection
	- Channels: SPI, UART, USART, AXI-Stream
	- Mappings: Address bus, AXI-MM, I$^2$C, GPIO
- The physical connection may not resemble the IO function
	- Audio devices may be memory mapped
	- Switches may be accessed over SPI

#### IO Performance: channel or mapping?
- We have two big performance metrics
	- Throughput: number of transaction per second
	- Latency: time to complete any one transaction
- In the context of IO these are:
	- Bandwidth: number of samples read or written per second
	- Access time: time to complete a single read or write
- Bandwidth is usually in competition with access time
	- To improve bandwidth we add buffering and pipelining 
	- To reduce access-time we remove intermediate buffers

#### Serial/Parallel Communication
- Cost and size matter too
- In parallel communication all the bits in a digital word are transmitted at the same time 
	- For a 32-bit word you need 32 wires
	- This present scalability and cost issues 
- In serial communication you send one bit at a time
	- Need fewer wires 
	- Timing closure is simpler 
	- Must include parallel <-> serial shift registers


# References