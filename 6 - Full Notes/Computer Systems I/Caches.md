22-12-2024 23:00

Status:

Tags: [[Computer Systems I]] [[RAM]]


# Caches

#### Caches:
- CPU needs data faster than DRAM can provide
- Caches are small blocks of fast SRAM located on CPU chip
- Memory requests go there, not DRAM
- Simplified example:

- ![[Pasted image 20241222230133.png]]


#### Latency:
- it is not just the data rates that are problematic
	- DRAM with a CL (latency) of 5 takes clock cycles to provide data or about 60ns 
	- fast static RAM takes more like 1ns
- DRAM ratings like CL=15 means 15 clocks per transaction
	- remember a 4Ghz clock cycle is 0.25ns!

#### Cache operation:
- CPU reads memory location
- address goes to cache
- if present, cache provides data (cache hit)
- If not present, block read required from main RAM to cache (cache miss)
- Then deliver data requested by the CPU
- don't think of it as cache "searching" for data - the mechanism is very simple!

#### Cache line:
- A chunk of data stored by the cache. Word/bytes are too small. Note modern typical line is 64 bytes

#### Cache design parameters:
- Size 
- Mapping Function needed - cache is smaller than main memory
- Replacement algorithm
- Write policy
- Block size
- Number of caches

#### Instruction/data split:
- they have different access patterns so to prevent two types of cache access:
- instructions are read only

#### Multi-level caches:
- big caches have longer latency so generally use smaller L1 then bigger L2 cache
- Multiple cores usually share a large level 3 cache to "shield" RAM from the cores
- This is typical multiple core design:

![[Pasted image 20241222231158.png]]

#### Cache mapping function:
- Needed because cache is smaller than main RAM
- blocks of cache are allocated to certain addresses
- Simplest method - direct mapped
- Most caches now associative 
- Don't need to memorise mapping functions


#### Summary:
- DRAM, SRAM used where appropriate
- Caches are needed to speed up access to DRAM
- They depend on sequential/local access
	- store cache lines of 64 bits
- Three levels of cache are used
- 95% cache hits mean less RAM access so it is much faster and multi-core access is efficient
- Code can take cache size into account for speed










# References