20-12-2024 14:31

Status:

Tags: [[Computer Systems I]] 


# Operating Systems 2

[[Operating Systems]]

#### Why do memory management?
- To make the user think there are an arbitrary number of processes running at the same time
- To make every process think it has infinite memory
	- Engineering interpretation of infinity:
	- Entire address space, 32 bit machine is about 4 GByte
	- Entire address space, 32 bit machine is about 16 EByte (Exa = $10^{18}$ roughly $2^{60}$)
- Virtual memory (VM) does just this

#### Swapping:
- The OS stores a queue of processes wanting to execute
	- Processes on a disk, queue in the kernel
- As space becomes available, the processes are loaded
- When a process finishes, it is removed
- A process may also be swapped out if it is stalled (e.g. waiting for I/O)
- Swapping involves disk I/O and could make problems worse!
- Involving VM instead of just swapping can improve performance

#### Partitioning: 
- Fixed size memory partitions
	- Typical usage implies logarithmic distribution of partition sizes is best
	- Easy to administer
- Variable size memory partitions
	- Memory is allocated as required
	- Fragmentation makes it harder to load incoming processes

#### Addressing in partitioning:
- Logical address:
	- Expressed as a location relative to the beginning of the program
- Physical address:
	- An actual address in main memory
- Base address:
	- Current starting location of the process (Process = Instruction + Data)

#### Paging:
- Fixed and variable size partitions are very inefficient
- Divide the physical memory into lots of small, equal chunks (frames)
- Divide the process into chunks (pages) of the same size as the memory frames
- The process of mapping pages => frames is efficient (in terms of memory)
  
#### Virtual memory:
- We can now load processes larger than the physical memory 
- Pages (not processed) swap in and out as required
- A single process offset is no longer enough
- We need a table of offsets for each page <=> frame mapping of each process: the page table
- Logical addresses now refer to a page, and the page table translates the base address (logical page) to a physical address (physical frame)

#### Demand paging:
- Each page of a process is brought in only when it is needed
- Principle of locality:
	- When working with a large process, execution may be confined to a small section of a program (subroutine)
	- It is a better use of memory to load in just a few pages
	- If the program references data or branches to an instruction on a page not in main memory, a page fault is triggered which tells the OS to bring in the desired page
- It is possible for a process to be larger than all of main memory!

#### Demand paging:
- Advantages:
	- More processes can be maintained in memory
	- Time is saved because unused pages are not swapped in and out of memory
- Disadvantages:
	- When one page is brought in, another page must be thrown out (page replacement)
	- If a page is thrown out just before it is about to be used the OS will have to go get the page again
	- Thrashing:
		- When the processor spends most of its time swapping pages rather than executing instructions

#### The table *itself* can be paged in and out:
- One page table per process:
	- A machine that has $2^{31}$ = 2 GByte of physical memory
	- 512 = $2^9$ byte frames => $2^{22}$ page table entries per process
	- The page table is held in virtual memory
- When a page is active, the relevant part of the page table must be accessible (i.e. in memory):
	- Multi-level page table hierarchy 
	- Hash tables 
	- Many different approaches

#### The translation lookaside buffer: 
- Every logical memory access can require two physical accesses:
	- Page table entry
	- Data
- Most virtual memory systems have a dedicated cache for the page table - the translation lookaside buffer or TLB

#### From logical to physical addresses:
- The page table can be in:
	- The TLB
	- Main memory
	- Disk
- The required data can be in:
	- Memory cache
	- Main memory
	- Disk
- The whole point of VM is to pre-emptively get the required data into the most accessible place
- Virtual memory and paging is invisible to the user

#### Segmentation:
- Another way in which addressable memory can be subdivided
- Usually visible to the programmer as a convenience for organising programs and data and as for associating privilege and protection attributes with instructions and data
- Segmentation allows the programmer to view memory as consisting of multiple address spaces or segments:
	- Segments are of variable, indeed dynamic, size
- Typically, the programmer or the OS will assign programs or data to different segments. The may be a number of program segments for various types of programs as well as number of data segments. Each segment may be assigned access and usage rights. Memory references consist of a (segment number, offset) form of address. 

#### Advantages of segmentation: 
- It simplifies the handling of growing data structures:
	- No guessing if the programmer doesn't know program size ahead of time
	- The data structure can be assigned its own segment. The OS will expand or shrink the segment as needed
- It allows programs to be altered and recompiled independently without requiring that an entire set of programs be linked and reloaded
	- This is accomplished using multiple segments
- It lends itself to sharing among processes:
	- A programmer can place a utility program or a useful table of data in a segment that can be addressed by other processes
- It lends itself to protection:
	- Because a segment can be constructed to contain a well-defined set of programs or data, the programmer or system admin can assign access privileges in convenient fashion


#### TAKEAWAY:
- Fragmentation and thrashing are undesired side-effects of memory management which hinder performance
- Swapping, partitioning and paging, are the fundamental processes that allow virtual memory management by the OS, creating the illusion of a much larger memory than the real, physical memory available.

# References