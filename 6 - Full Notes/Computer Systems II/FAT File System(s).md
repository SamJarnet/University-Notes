2026-05-17 18:25

Status:

Tags: [[Computer Systems II]]


# FAT File System(s)

#### Why file systems differ from memory management
- In memory management (RAM), allocated memory is always consecutive - malloc returns one pointer to a contiguous block. File systems deliberately avoid this. 
	- If files had to be stored consecutively, extending a file (e.g. saving a longer document) would require copying the entire file to a new location with enough free space after it. That is obviously terrible - so file systems use non-consecutive blocks (also called clusters) that can live anywhere on the device.
- The trade-off: managing non-consecutive blocks is much more complex. You need metadata to track:
	- Which blocks belong to each file, and in what order
	- Which blocks are currently free
	- The file's exact length (the last block is rarely full)

#### Why FAT is still widely used
- Low RAM overhead
	- Designed when RAM was precious. The FAT itself lives mostly in RAM but is compact. Still ideal for embedded systems (microcontrollers, digital radios, IoT). Early PCs had little RAM, and embedded systems still often do.
- Universal Compatibility
	- Every OS can read FAT. Format a USB stick with FAT and plug it into Windows, macOS, Linux it just works. No other file system has this reach.
- Simple to implement

#### CP/M - the predecessor 
- Control Program for Microcomputers is the ancestor of FAT
- The metadata mistake
	- CP/M defined the file system internals but never standardised the boot record/partition metadata. Result: two CP/M machines from different manufacturers, both using the same processor and the same file system, couldn't exchange disks - incompatible metadata
		- FAT fixed this: it standardise d the master boot record and partition layout, so any FAT-formatted disk works in any machine
- Software skew
	- Early CPUs were slow. By the time the CPU finished processing block 1, block 2 had already spun past the read head on the disk. 
		- Solution:
			- Intentionally place blocks out of order (e.g. 1, 7 , 13, 19) so the CPU has time to prepare before the next needed block arrives. 
		- Nowadays;
			- We want consecutive blocks for speed - SSDs make this irrelevant. 
- CP/M legacy still visible today. The C: drive letter notation, the .txt / .exe three-character extension, and the 32-byte directory entry were all CP/M ideas that FAT inherited

#### FAT partition layout 
- A disk has a Master Boot Record (first sector), followed by partitions. Inside each FAT partition, the layout is always
	- Volume ID  (1 sector)
	- Reserved  sectors
	- FAT 1  primary
	- FAT 2 backup copy
	- Root Dir
	- Files & Directories  (clusters)
	- Unused
- Volume ID / Boot Record 
	- First sector of the partition. Contains bytes/sector, sectors/cluster, number of FATs, and more. Ends with magic bytes AA55 as a validity check - if you read something that claims to be a FAT partition and AA55 isn't there, stop. Don't corrupt the disk./
- Why two copies of the FAT?
	- People used to take out the disk mid write. FAT uses a two-phase updates: write to FAT1 first -> do the operation -< update FAT0. If power dies between steps, FAT0 is still consistent. This redundancy protects against the FAT getting corrupted.
- Why unused space at the end?
	- Two reasons:
		- Flash/SSD drives have limited write cycles - keeping ~30% free allows the wear-levelling algorithm to spread writes.
		- Historically, if your disk started dying you'd buy a new one - it might be slightly smaller, so having spare space meant you could still copy everything across
- Reserved sectors
	- Originally intended as optional space for clever tricks like copy protection (scratching specific sectors, then checking they're unreadable). In practice, mostly unused, viruses did exploit them.

#### Directory Entries
- Each entry is 32 bytes. The directory is just an array of these. When you ask for a file by name, the OS scans the directory looking for a matching name, then reads the start cluster and file size.
- FAT-16 directory entry (32 bytes)
	![[Pasted image 20260517201646.png]]
	- Start cluster (tells you where to look in the FAT) and file size (tells you how much of the last block is actually data)
- First byte of the filename - special codes
	![[Pasted image 20260517201945.png]]
	- Deleting a file only changes that one byte and marks its blocks available in the FAT - it does NOT erase the data. this is why file recovery tools work, and why "deleting photos in front of the security guard" doesn't actually destroy them. On a freshly formatted card with no fragmentation, you can reconstruct everything: you will still have the start cluster and file size, so you just read consecutive blocks until you hit the file size.
- Attribute byte (8 bits)
	![[Pasted image 20260517202250.png]]
- The  "all special bits set" combination (Volume Label  + System + Hidden + Read-only) was unused in normal use, so Microsoft exploited it for VFAT long filenames - the old FAT driver would silently ignore it, giving backwards compatibility

#### The File Allocation Table
 - The FAT is a single flat array of numbers. Its index corresponds to a cluster number on the disk. The value at each index tells you what to do next
 - Fat entry values (FAT-12 Example)
	 ![[Pasted image 20260517202610.png]]
- The double duty trick
	- The FAT does two jobs at once: 
		- It stores the cluster chain for every file AND indicates which clusters are free (value 0x000). This means to find a free block, you can scan the FAT looking for a 0x000 entry - no separate free-block bitmap needed.
-  How to read a file:
	- 1. Look up the filename in the directory -> get start cluster (cluster 3) and file size
	- 2. Read cluster 3 from disk -> that's the first chunk of data
	- 3. Look at FAT$[3]$ -> if it's, say, 0x005, then the next cluster is 5 
	- 4. Read cluster 5 from disk -> next chunk of data
	- 5. Look at FAT$[5]$ -> if it's 0xFFF (EOC), this is the last block
	- 6. Use the file size to know how many bytes in this last block are real data (the rest is garbage)
- How to extend a file:
	- 1. Scan the FAT from the beginning for the first 0x000 entry - that's your free block
	- 2. Update the current last block's FAT entry to point to this new block (instead of EOC) 
	- 3. Set the new block's FAT entry to EOC (0xFFF)
	- 4. Update the file size in the directory entry.
	- This all happens in RAM (the FAT is loaded into memory). The updated FAT must be written back to disk before the device is ejected - hence the "safely remove hardware" requirement.
- Special FAT entries:
	![[Pasted image 20260517203342.png]]
- Partition state (FAT entries 0 and 1 are special)
- Entry 0 = media type (floppy cs hard disk). Entry 1 = partition state: FFFF = clean(set on shutdown), FFF8 (set when writing begins). If the OS mounts a FAT and sees "dirty", it knows the previous session didn't shut down cleanly - time to run fsck / chkdsk.

#### FAT12, FAT16, FAT32 - why the variants exist
- The number refers to the bit width of the entry in the FAT. More bits = more possible clusters = larger maximum disk sizes
	![[Pasted image 20260518112118.png]]
- Why do FAT file systems have file size limits? 
	- Because FAT entry width limits how many cluster numbers you can address, and the cluster size is bounded by physical write performance. Increase the entry width and you can increase both limits.
- FAT32 note:
	- Only 28 bits  used
	- The top 4 bits are reserved and must be masked out before interrupting the value. Also stored in little-endian order - least significant bit first

#### Block (cluster) size trade-offs 
- Typical modern block size: 4KB 
- Bigger Blocks - pros
	- Less metadata needed (fewer FAT entries)
	- Consecutive reads are faster (especially on spinning disks)
	- Less overhead per file
- Bigger blocks - cons
	- Internal fragmentation - last block wasted. A 1-byte lock file wastes (block_size -1) bytes
	- With a 500 KB block, an empty lock file wastes half a megabyte
	- Also limits how many files you can address with a given FAT entry width

#### VFAT - long file names
- FAT12 and FAT 16 limited names to 8+3 characters. Microsoft added long name support in a backward-compatible way: use an attribute combination that was never valid in real files (Volume Label + System + Hidden + Read Only all set simultaneously) to store extra directory entries  with the long name. Old FAT drivers see this invalid combination, shrug and skip it. New drivers read the long name from these extra entries.

#### Flash Memory complications
- Flash has two properties that clash with FAT
	- Limited write cycles - each cell can only be written ~ 10,000 - 100,000 times before failing.
	- Erase-before-write - you can't flip a bit from 0 -> 1 without erasing the whole block (often 512 bytes or more). Changing one bit means read-erase-modify-write.
- The FAT and directory entries live at fixed locations and get updated constantly. This causes those sectors to wear out faster. Solutions include wear-levelling (the controller rotates where logical blocks map to physical blocks) and leaving significant free space (gives the wear-leveller room to manoeuvre). The lecturer says he keep his phone under 70% full for this reason
	- One emerging fix:
		- Battery packed RAM to cache metadata, then jump directly to wherever it lives on flash - avoiding fixed location problem entirely.

#### Identifying the FAT type
- Microsoft recommended algorithm - look at the numbers of clusters c:
	- if c < 4085 -> FAT12
	- else if c < 65525 -> FAT16
	- else -> FAT32
- This works because you cannot represent a cluster number larger than 4085 in 12 bits, so any volume with fewer clusters must be FAT12. A robust test is more complicated, but this simple one is what the Microsoft spec recommends.
- FAT32 root directory is located in the cluster area (not a fixed location before the data) - another tell.

#### Exam questions
- How does the OS find file X?  
	- Scan directory entries for a name match -> get start cluster + size -> follow FAT chain -> use size to trim last block
- How does the OS allocate a new block?
	- Scan FAT for first 0x000 entry -> write its index into the current last block's FAT entry -> mark it as EOC -> update directory size.
- Why does FAT have size limits?
	- FAT entry bit-width caps the number of addressable clusters; cluster size cap causes internal fragmentation.
- Why are deleted files recoverable? 
	- Only the first byte of the directory changes (to 0xE5); data blocks are marked free but not zeroed
- What is software skew? 
	- CP/M era trick: intentionally non-consecutive block ordering so slow CPUs had time to process each block before the disk's next block arrived.
- Why two FATs?
	- Redundancy + two-phase update (write FAT1 first, then FAT0) for crash consistency.
# References