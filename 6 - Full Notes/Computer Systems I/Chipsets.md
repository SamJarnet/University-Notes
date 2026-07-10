27-12-2024 13:01

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Chipsets

#### Why?
- Chipsets link all the components of typical computers 
- It changes every few years

#### Classic PC architecture:
- Chipset joins up the main buses in the system
- North=Fast
- South=Slow
- RAM data had to pass through the North Bridge 

- ![[Pasted image 20241227130311.png]]

#### e.g. older Intel Architecture:
- FSB connection between CPU and Northbridge
	- Memory Control Hub
- Northbridge handles "primary" PCIe to video/[[GPU]] and D[[RAM]]
- PCIe x16 bandwidth at 8 GB/s
- Southbridge handles other peripherals
- Old architectures used multiple CPU sockets
- Problem is needing very high bandwidth to RAM from multiple CPU chips

#### Newer Server motherboards:
- More RAM (e.g. 1TB RAM)
	- And slots for each processor
- ECC RAM - error correcting
- Onboard RAID
- Dual/quad sockets for many CPUs
- 10Gb/s Ethernet
- Web accessible

#### UltraPath Interconnect (UPI):
- Intel's proprietary high speed link
- Point to point link between CPU chips and to chipset
- Around 20GiB/s per link
	- Intel desktop Processors typically have two or three UPI links 
- Handles cache-coherency

#### Basic Input/Output System (BIOS):
- Firmware on the motherboard
- Hardware initialisation/start-up test
- Booting
- Stored in Flash (so it can be updated)
- MS-DOS used I/O functions in BIOS to help standardise PCs
- finds a boot loader on disk/CD/USB
- Loads first sector of disk into RAM, then runs that code to boot

#### UEFI:
- Replaces old BIOS
- CPU-independent: ARM/Intel
- Supports 64 bit systems
- Boot services and Runtime services
- Date, time, NVRAM
- GOP - graphics output protocol
- Does not rely on boot sector (uses NVRAM data to boot OS)

#### Raspberry pi 5 chipset! 
- “RP1” Handles I/O instead of the processor chip 
	- Analogue things 
	- Ethernet, camera/LCD, USB, GPIO 
	- SPI, I2C, serial, PWM



#### Summary:
- Chipsets define the paths/buses
	- Scale up to muti-processor multi-chip
	- PCIe dominates
- Bandwidths of the various sub-systems are work knowing (roughly)

# References