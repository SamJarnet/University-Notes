22-12-2024 23:21

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Buses

#### Buses:
- Single and multiple BUS structures are most common:
	- Control/Address/Data bus
	- Peripheral Component Interconnect Express (PCIe)
	- Serial ATA (SATA)
	- Universal Serial Bus (USB)

#### What do buses look like?
- Some parallel lines on circuit boards/ICs 
	- plug in connectors on motherboards
	- sets of wires, fibre
	- backplane
- Some are serial interconnections
	- e.g. SATA, PCIe, USB
	- May only have one device at each end

#### What is a shared Bus?
-  A common communication pathway
- Three types of bus lines in a conventional parallel bus:
	- Data lines
	- Address lines
	- Control lines
- Signals might be seperate, multiplexed serialised...
	- e.g. a number of channels in one bus
	- e.g. a serial connection

#### Parallel Data Bus:
- Width is important factor for performance for a parallel bus
	- 8, 16, 32, 64 bit... etc.
	- e.g. if data bus is 8 bits wide and each instruction is 32 bits long - processor must access the memory 4 x
	- So CPUs internally use 64 bit paths

#### Address bus:
- Identify the source or destination of data
	- e.g. CPU needs to read an instruction (data) from a given location in memory
- Bus width determines maximum memory of a system
	- Most modern CPUs have a 48 bit virtual address
		- more than enough for addressing desktop RAM

#### Control Bus:
- Control and timing information
	- Controls access to the data and address lines
	- Timing Signals indicate the validity of data and address information
- Typical control lines include:
	- Memory read/write signal 
	- I/O Port read/write signal 
	- Transfer Acknowledgement 
	- Bus request/grant 
	- Interrupt request/acknowledgement 
	- Clock signals
	- Reset
- mostly hidden from programmer/user 


#### Using a shared bus:
- Obtain the use of the bus
	- Only one module can use the bus at any one time
	- Bus control is handled through Arbitration
- Transfer data and/or requests
	- Data and instructions may be on dedicated lines
	- Multiplexing necessary if data/instructions share lines
- Synchronise and/or acknowledge
	- ensure that recipient is ready for data
	- ensure that recipient received data


#### Single Bus Problems
- Lots of devices on one bus leads to:
	- Propagation delays
		- Long data paths mean that co-ordination of bus use can adversely affect performance
		- If aggregate data transfer approaches bus capacity 
- Different devices may work at different speeds
- Most systems use multiple buses to overcome these problems


#### Timing:
- Co-ordination of events on bus
- Normally Synchronous 
	- Events determined by clock signals
	- Control bus includes clock line 


#### PCI express: PCIe:
- Serial bus with multi - GiByte/s "lanes"
	- Speed depends on version 1-5 roughly:
		- v3 1GiB/s
		- v4 2GiB/s
		- v3 4GiB/s
- Use more than lanes for a GPU card (16 is roughly 16GiB/s)
	- Or use one for small simple card!
- PCIe mini cards for laptops (1 lane, USB & compatibility)

- Packets are sent over serial links
- ACK/NACK protocols maintain data safety
- There are a few other signals and power on the normal PCIe socket]
- Is like a network - with layers and addressing

![[Pasted image 20241223142112.png]]

#### PCIe as an SSD interface:
- NVM Express (NVMe), M.2
	- Fast! (7GB/s read 5GB/s write typical on PCIe4)
	- Supports long command queue (64k)
- directly attached to the PCIe

#### Hard disk connectivity:
- SATA - serial bus 3-6 Gbit/s so about 500MB/s
- SAS (servers) 12 Gbit/s so about 1.2GB/s, 22 Gbit/s emerging
- Fibre channel (can pass other protocols)
	- Good for long distances like 10-50km!
	- 100MB/s to 25GB/s
	- These all link a disk to one controller


#### SCSI - used in server storage:
- Was the main server disk bus in the 1980/90s
	- 1 to 15 devices per channel/ribbon cable!
	- 10 to 640 MB/s
- iSCSI common now - over networks
	- uses TCP/IP
- SAS - serial attached SCSI
	- Very common now


#### SAS – serial attached SCSI
- fast serial SCSI, compatible with latest SATA, 3-6Gbit/s
- Very flexible due to the layers of the protocol


#### Serial Peripheral Bus: [[SPI Bus]] 
- As used in the lab for the external ADC 
- Signals: clock, output, input, select 
- Clock around MHz 
- Select is used to choose an IC


#### Universal Serial Bus (USB):
- Ideal for low-speed to high I/O devices
- Expandable:
	- allows up to 127 devices
	- simple design and configuration
		- single cable design, also supplying power
		- support for real-time devices and device classes
- USB2: 480Mbit/s
- USB3: 4.8 - 10 - 20 Gbit/s
- USB4: 10-40 Gbit/s (2019)

#### USB hardware:
- USB systems assumes a root hub connected to the main bus
	- Further hubs can be connected to this hub, forming a tree topology
- Cable contains four wires:
	- 2 data lines
	- 1 power (+5V) and 1 ground
- Data transmitted as:
	- "0" is transmitted as a voltage transition
	- "1" is the absence of a transition
	- Thus, a sequence of "0"s forms a regular pulse stream

#### USB Signals:
- Every 1.00 +- 0.05 msec, the root hub broadcasts a new frame
	- If no data to be sent, just a "Start of Frame" packet is sent
	- Data associated with one addressed device, either to or from hub
- Four kinds of frames:
	- Control
		- Used to configure devices and inquire status
	- Isochronous
		- For real-time devices where data should be sent/received at precise intervals
	- Bulk
		- For large data transfers
	- Interrupt
		- USB does not support "interrupts", so this frame is used for regular polling of devices, e.g. polling a keyboard every 50ms.

#### Motherboard [[Interconnections]]:
- high speed links to chipset from one or more CPU packages
- DMI replaced with UPI in some later high-end processors 2017 -
- These links are very similar to PCIe







# References