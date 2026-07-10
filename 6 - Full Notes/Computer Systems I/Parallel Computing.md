27-12-2024 13:26

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Parallel Computing

#### Flynn's Taxonomy
- Classification of computer architectures
	- Proposed in 1966
	- Extended in 1972
- Four classifications based on number of instructions and data streams
- But missing vector processing

![[Pasted image 20241227132855.png]]


#### SIMD extensions:
- SIMD processing
	- i.e. do the same thing to many data objects
- 64/128/256 bit Words are large enough for many bytes packed inside
- Needs special hardware in CPU
	- e.g. an extension to x86 in 1999 (Pentium III)
		- Streaming SIMD Extensions (SSE)
- Needs special software too

#### SSE uses:
- Image processing - multiple pels at a time
- video processing - processing blocks 
- array/vector processing
- text processing (especially new $<XML>$ instr. )
	- 1.25 to 1.7 speed-ups reported
- General speed-up depends on application
	- Compilers can detect code which can use SSE
	- Read the auto-vectorisation link

#### Example - Linux Boot:
- Linux tests to see how fastest RAID calculations can be done calculations can be done - look at boot messages with dmesg:

#### SSE - Streaming SIMD extensions for x86:
- 128-bit registers that can be packed with various data types
- 64-bit x86 CPUs have 16 of these registers
- Extra ~50 instructions for SSE operations
- AVX extends SSE:
	- 256-bit registers
	- Three-operand instructions
- AVX-512: 512-bit registers



#### SSE example with 256 bits 
- Eight 32-bit floating point numbers packed into a special register 
- Processed together 
- Then unpacked

- ![[Pasted image 20241227134116.png]]

#### SIMD: CUDA & GPU processing:
- GPUs have lots of "cores"
	- RTX 4090 has 16384 CUDA "cores"
- Processing on a GPU uses a SIMD model
	- through NVIDEA call it Single instruction, multiple thread
	- e.g. CUDA uses thread warps, with each warp executing the same instruction



#### Symmetric Multiprocessors - SMP:
- A MIMD system
- Multiple CPUs (or cores) share main memory and I/O 
- Hardware manages contention
- Increases performance especially multiuser/thread
- Reasonable scalable until bus is saturated

#### Typical SMP System:
- Each processor has its own L1 and L2 cache
- Connected by a system bus, crossbar switch or other interconnect
- Main memory, I/O, etc are also connected to the interconnect

#### Heterogenous Multi-Processing:
- Combine big performance cores with little energy efficient cores
- "Big" cores only used when performance is necessary, "little" cores used for most tasks
- Needs operating system support to fully leverage

#### Simultaneous multithreading (SMT) / Hyper-threading:
- Hardware multi-threading on superscalar CPUs
	- Think logical cores. i.e. one physical cores can be used as two logical ones
- Executes multiple instructions at the same time using redundant execution units in the processor
	- e.g. 2-way SMT is common Intel (Hyper-threading) and AMD
	- Improves performance by ~30%

#### Supercomputers:
- typically best technology of the time
- vector or SIMD common
- high power, clever cooling, etc.
- Clusters, clouds

#### Some important terms:
- Data parallelism: split the data to make independent parallel tasks
- Task parallelism: split the code up - e.g. threads on seperate CPUs
- Embarrassingly parallel problem: very easy to split task into parallel subtasks
	- e.g. graphics, millions of images, bitcoin mining




# References