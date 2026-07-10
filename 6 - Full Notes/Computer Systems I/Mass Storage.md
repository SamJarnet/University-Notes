23-12-2024 18:45

Status: 

Tags: [[Computer Systems I]] [[Buses]]


# Mass Storage

#### Types of mass Storage 
- Magnetic Disk 
- Solid State disks 
- Optical 
	- DVD, Blue Ray 
- Magnetic Tape

#### Magnetic Disk:
- Metal/glass/ceramic disk coated with magnetisable material
- Range of packaging: 2.5", 3.5", hot-swap
- Still the best value online storage
- Capacity grows with each generation

#### “Winchester” Hard Disk:
- Developed by IBM in Winchester (USA) in 1956 (5 MB!) 
- Sealed unit 
- One or more “platters”
- Heads fly on boundary layer of air as disk spins 
- Very small head to disk gap 
- Now Fairly robust

#### Multiple Platters:
- One head per side
- Heads are joined and aligned
- Aligned tracks on each platter form cylinders
- Data is striped by cylinder
	- reduces head movement
	- Increases speed (transfer rate)
#### Disk head:
- tiny, light read/write arm and head
- Was coils, now is a magnetic sensor

#### Data Organisation and Formatting:
- Concentric rings or tracks
	- Gaps between tracks
	- Reduce gap to increase capacity
	- Same bits per track (variable packing density)
	- Constant angular velocity
- Tracks divided into sectors of 512B or 4kiB
- Minimum block size is one sector

#### HDD Speed determined by:
- Seek time
	- Moving head to correct track
- (Rotational) latency (e.g. 4ms)
	- Waiting for data to rotate under head
- Access time = Seek + Latency
- Transfer rate
	- e.g. average access time 8ms for a modern disk

#### Hard disk Throughput:
- Controllers have different speeds and optimisations (many optimise requests)
- Throughput off disk may be 150MB/s, but burst over bus faster (e.g. 6Gbit/s SATA, 12 Gbit/s SAS)
- Big disks now can average 200MiByte/s
- Don't confuse connection speed with actual throughput (e.g. 6GiBit/s SATA is roughly 600MiByte/s)

#### On-Disk cache:
- Modern disks have 8-512 MB on-board RAM buffer/cache
- Used to store whole tracks and cache r/w
- acts as a buffer between disk and external I/O

#### Fast and big Disks:
- Current disk range:
	- Around 32TB are largest
	- 10-15 k rpm fastest spin
	- Sustained data rates 150-250 MiBytes/s
	- average access time 3.6 - 8ms
	- Around 10W power

#### Mean time between failures (MTBF):
- Around 1000000 hrs = 114 years!
- e.g. "annualised failure rate" of fast disks = 0.5%
- so two disks in RAID0 has half the MTBF
- But if you have you have 100 disks you expect one to fail
- And double failures probable
- Platter, heads, electronics, connectors, enclosure...


#### Solid State Drives (SSD):
- Non volatile NAND logic (fast) or Flash based
- fast ACCESS TIMES (SATA 1ms NVME roughly 0.1ms)
- Near "zero" latency compared to HDs
- sequential Read speed: 500-7000MiB/s
	- depends on PCIe version
- Transactions/s (IOPS) often quoted (e.g. 90000)
- max about 18TiB at the moment
- more shock resistant, silent
- lower power (roughly 2W c.f. 6W HD = good in laptops!)
- But expensive per GByte compared to HD


#### SSD characteristics:
- can only write approx. Millions of times
	- wear levelling - spreads the writes around so one area is not worn out
	- overprovision - spare storage to use if blocks fail
- file systems consider SSD issues:
	- TRIM command to tell SSD which blocks are not needed and can be "erased"
	- erase normally only works on blocks
- they need up to date firmware and drivers
- A very full SSD can wear-out the remaining space faster

#### SSD architecture:
- Controller does interface, addressing, wear levelling error detection/correction, bad block management
- To change some bytes a Block has to be read and modified, then written back

#### PCIe is the best SSD interface:
- SATA is not fast enough (roughly 600MiB/s) so:
- MVME, in M.2 format using PCIe :
	- Fast
	- Supports very long command queue (64k)
- directly attached to PCIe 2-4 lanes
- Usually have onboard [[RAM]] [[Caches]]

#### Blu-Ray:
- Use tiny laser - hence smaller features
- 15-30GiB still useful for offline storage/transfer
	- 128GiB 4 layer versions exist
- Can read at 70MiB/s


#### optical Jukeboxes 
- 100s TB per box! Typically Blu-ray
- e.g. 6s disk change time 
- e.g. 500 slots, 10 drives

#### Magnetic Tape – its not dead! 
- Large – 12TB to 36TB
- Serial access but good for backups 
- speed often quoted in GB/hour 
	- LTO is ~ 1GiB/s ! 
- Cheap per Tbyte 
- Backup and archive

#### Tape Autochangers 
- hold banks of tapes –> exabytes (10^18 bytes) 
- Multiple drives 1-144 
- Required for unattended backup and cycles

#### iSCSI- Internet Small Computer System Interface
- uses TCP/IP over normal ethernet etc 
- typically uses isolated network (for bandwidth) 
- can use an offload-processor card to save [[CPU]] time 
- allows remote and very flexible storage arrays

#### SAN – storage area networks 
- like disks – block accessed 
	- i.e. not like NAS which is a file server 
- fast and low latency 
- Starting to use 16Gbit/s fibre channel 
- Can use 12 HDD or SSD

#### Hierarchical Filesystems 
- Use RAM, Disk, RW optical, tape
- Automatically move files down/up media!

#### Redundant Array of Inexpensive Disks (RAID):
- RAID 0:
	- No redundancy!
	- Data striped across all disks
	- Increase speed
		- Multiple data requests probably not on the same disk
		- Disks seek in parallel
		- A set of data is likely to be striped across multiple disks
	- Size is N * Disk Size
- RAID 1:
	- Mirrored Disks
	- Data is striped across disks
	- 2 copies of each stripe on seperate disks
	- Read from either
	- Write to both - size is size of one disk
	- Recovery is simple
		- swap faulty disk and re-mirror
		- no down time 
	- Expensive
- RAID 5:
	- Parity striped across all disks
	- Round robin allocation for parity stripe
	- Size is (N-1) * Disk Size
- RAID6: 
	- double parity writes
	- CAN tolerate TWO disk failures! 
	- Much more reliable but Size is (N-2) * Disk Size

#### Rebuilding:
- When a drive fails - the system has to rebuild!
- This can take a long time!
- System can still perform OK
- Hot-swap drives mean no downtime!
- Or a "hot spare" drive is always in system for automatic rebuilds


#### Filesystems:
- File structure on top of disks
	- Very important for performance and safety
	- Controls permissions and other metadata
- Windows uses NTFS
- Linux servers use ext4 or ZFS
- ZFS is very sophisticated:
	- Choice of RAID styles
	- can use SSDs as cache drives
	- Checks data integrity
	- Encryption option




# References