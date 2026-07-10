22-12-2024 15:08

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Modern CPU Architectures

#### What is a multicore CPU?
- originally multiple CPU chips were pot onto motherboards to improve speed
- Eventually multiple "cores" could be put into one package 
	- some servers still use multiple CPU chips
- multi-core is very efficient as the integration is all one one chip

#### Improvements:
- Instructions per clock (IPC)
- wider decoding (32 instr/cycle)
- bigger micro-Op cache (4k)
- more exec ports (12)
- out of order window increase
- big load/store queues (>100)

#### Cache changes:
- Caches are fast SRAM which store most recently access bytes from DRAM
- caches hate "widely spaced" address accesses
	- now "better stride prefetching in L1"
	- "predictive line-write" in L2
- Bigger caches (1-2MB for L2)

#### Hyperthreading:
- A core can "look like" two cores:
	- Needs extra infrastructure (5% more silicon area)
	- But share execution units/caches
- Separate threads can run (but not same speed-up as more cores)
- Some benchmarks are 15-30% better
- Some new CPUs are deleting this in favour of more cores

#### Power management:
- separate microcontroller looks after power
	- can completely shut down cores
	- can boost clock when needed (and cool enough)
- Very important for performance and power saving

#### Turbo Boost:
- Clock speed increased for short bursts or if only one core is in use:
	- depends on temperature/power
- used on most CPUs 
- e.g. a "3.6GHz" CPU:
	- 1 or 2 cores active 5GHz
	- 3 or 4 cores active 4.8 GHz
	- 5-8 cores active 4.7 GHz
- Core ultra 9 boosts to 5.7GHz (P) but normal 3.7 GHz


#### Integrated memory controller:
- RAM controller was previously on the motherboard chipset
- On-chip DRAM interfaces reduces latency

- ![[Pasted image 20241222152347.png]]

#### Non Uniform Memory Access (NUMA)
 - describes multiprocessor systems with seperate blocks of RAM
 - Local RAM is fast 
 - Remote RAM is accessible but slower 
 - Mechanisms can include ccNUMA (cache coherency)
 - Helps reduce bottlenecks
 - Useful with large number of cores or clusters
 - Also happens on multi-chiplet and meshed cores

- ![[Pasted image 20241222152608.png]]


#### Vector instructions (e.g. SSE):
- Vector unit has progressed every few years - also provides extra instructions:
	- CRC (error checking) 
	- text processing instructions (e.g. for XML)
- Advanced Vector Extensions (AVX): 
	- 256 and 512 bit wide vector words 
	- Can sometimes be used instead of a GPU – needs the right software!

#### Neural Processing Unit (NPU):
- CPUs gained specialist units 
- Neural net calculations are not exactly like graphics ops, so a matched design is faster
- MAC (multiply accumulate)
	- is a = a + ( b x c )

#### Other special units (depending on model):
- Data streaming (moving data)
- Encryption/decryption:
	- Think how many SSL secure connections you make!
- Matrix accelerators
- Virtualisation support

#### Intel "hybrid architecture": 
- Use a mix of **P**erformance and **E**fficiency cores 
- Processes needing less performance can run on E Cores and save power/heat
- E cores don't have big execution units or so many features
- E is roughly a quarter of the silicon area of a P core 
	- Core Ultra 7 can have 6P 8E 
	- Core Ultra 9 can have 8P 16E 
- Windows 11 has "thread director" to manage Big/E core processes 
- Linux also has knowledge of P/E cores

#### Newer generation Intel CPUs 
- Moving to PCIe v5 (~4 GB/s per lane)
- DDR5 ram support (up to 5.6GT/s) 
- Some can boost clock to ~6GHz
- 7nm process - so not caught up with AMD (4nm) or Apple yet (3nm)

#### Apple’s ARM-based M* 
- Uses ARM’s “Big-Little” architecture – used in phones/tablets previously 
- fast P cores plus power efficient E cores 
- Rely on a smarter scheduler 
- M1 had DRAM bonded on top of the processor chip (like some Pis) 
- M3 is 12P 4E down to 4P 4E 
- 3nm process means chips can be tiny, lower power or have a lot of modules
# References