22-12-2024 22:39

Status:

Tags: [[Computer Systems I]]


# RAM

#### Memory Characteristics:
- Location
- Capacity
- Unit of transfer
- Access method
- Performance
- Organisation

#### Capacity:
- Expressed as Bytes

#### Unit of Transfer:
- Internal
	- Usually governed by data bus width (e.g. 64 bit)
- External
	- Usually a block which is much larger than a word
- Addressable unit
	- Smallest location which can be uniquely addressed


#### Making RAM:
- Fast Static RAM can be made with logic gates
- DRAM is not like this 

#### Performance:
- Access time:
	- Time between presenting the address and getting the valid data (often states as N clocks) typically nanoseconds
- Memory Cycle time:
	- Time may be required for the memory to "recover" before next access
- Transfer rate:
	- Rate at which data can be moved - typically gigabytes/s

#### Physical types:
- Semiconductor:
	- SRAM
	- DRAM
	- Flash
- Magnetic, bubble, optical etc.
	- Ferroelectric RAM FRAM exists! fuck this course
	- Lots are still under development

#### Physical Characteristics:
- Decay
- Volatility
- Erasable 
- Power consumption


#### Storage Hierarchy List 
- Registers
- L1 Cache
- L2 Cache 
- Main memory “memory” 
- Disk cache (confusingly in main RAM and on disk controller)
- Disk, Flash/SSD, Optical Tape “mass storage” 

#### Dynamic RAM (DRAM):
- Bits stored as charge in capacitors 
- Charges leak so need refreshing even when powered
- Simpler construction
- Smaller per bit
- Less expensive 
- Slower (0-60ns)
- Used in our main RAM

- Capacitor charge represents a bit
- "switch" connects it to the read or write circuit


#### DRAM refresh:
- Each bit discharges over time and is boosted back to by the refresh
- This is a disadvantage of DRAM - but density is very high

#### DDR4 throughput:
- A DDR4-3200 DIMM reads 3200M x8 per second
- 25GB/s
- Reading 64 bytes a sequence starting with an initial 8 bytes can be done very quickly

#### DDR5 - current standard:
- 2 x DDR4
- faster clocks - up to 4GHz - more bandwidth
	- 4800 to 8800 M transactions/second
	- A transaction is still 8 bytes
	- so around 4800x8 38 GiB/s up to 70GiB/s 
- Two independent 32 bit channels
- Some error correction built in
- Lower voltage (1.1V) - 20% less power
- Can burst read 64 bytes
- Up to 96GB DIMM

#### Static RAM (SRAM):
- Bits stored as on/off gates (e.g. using 4-6 transistors)
- No charges to leak, no refreshing needed when powered
- More complex construction, larger per bit
- More expensive per MiB (about 100x)
- Faster (0.5 to 10ns)
- Good for Cache and embedded RAM
- Only used as main RAM on microcontrollers

#### Read Only Memory (ROM):
- Permanent storage
- Hardware supports library subroutines
- Systems programs (BIOS)
	- In reality very little is actually completed read-only now its just "read-mainly" but writeable

#### Banks, Ranks and Interleaving:
- Most [[CPU]]s use TWO 64 bit channels to the DIMMs
- Using four DDR4 DIMMs increases bandwidth and decreases latency to/from cache as accesses can be interleaved
- Triple channel motherboards can use three DIMMs in parallel (usually server/workstation)

#### Error Correction:
- DRAM can loose data
	- e.g. 25k failures per Mbit per billion hours
	- Important on servers and high RAM workstations 
- Hard failure:
	- Permanent defect - the most common
- Soft error:
	- Random, non-destructive
	- No permanent damage to memory
- Detected (fixed) using Error Correcting Code (ECC)
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  


# References