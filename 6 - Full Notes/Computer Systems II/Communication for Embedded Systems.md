2026-05-06 15:46

Status:

Tags: [[Computer Systems II]]


# Communication for Embedded Systems

#### Contents
- Wired Communication
- Serial Communication: UART
- Serial Communication: SPI
- Serial Communication:  I$^2$C 
- Serial Communication: CAN

#### Communication 
- Transmit information to remote location over some medium 
	- Wired Communication 
		- In circuit 
		- Among devices
	- Wireless Communication
		- Nearby 
		- Long range

## Wired Communication 

#### Physics Background: Capacitance 
- Signals are transferred as a change of voltage or current over time
- At least two conductors are required
	- Don't wire things up with a single wire
- Two conductors are isolated from each other -> capacitor 
- Frequency-dependent resistance ($X_C$) across a capacitor
	![[Pasted image 20260506155218.png]]

#### Physics Background: Fourier Series
- Arbitrary waves can be viewed as weighted sum of sine waves of different frequencies.
- Digital square waves need very high frequency components 

- Capacitors can't act like super precise digital square waves
- Wire length increase -> more capacitance/time to charge/discharge. More insulation -> take more time
- The capacitor only starts charging when its gets that binary signal. There will be a delay and it gets worse with length

#### What is information?
- Quantification of Information -> Entropy
- Information content of a message is its surprise value
	- The more unexpected the information is for the receiver, the more information it holds
	- Exploited in compression to get rid of information not noticeable/surprising (repeat colour, frequency)
#### Some communication questions
- How do we recognise a message?
	- Standard protocol for start/end message bits
	- Radio: multiple frequencies transmitted. Find the difference between signals to work out signal (ghost/implicit noise)
- How are communicating unit connected?
	- Point-to-point (two units wired up directly) vs bus (multiple units communicate with hub)
	- Duplex (two can talk at the same time, e.g. phone)
	- Half-Duplex (two can talk but when you talk you can't hear, e.g. walkie talkie)
	- Simplex (one side talk, other side just listens, e.g. radio station)
- How is control communicated?
	- Reserve signals for control? Specific frequencies?
- How can we guarantee realtime behaviour?
	- Minimise delay
- How can protocols be made reliable?
	- Make sure noise doesn't throw of information. Maybe use parity bits, checksums or other approaches.

## Serial Communication 
#### UART
- We used this in the PICOs
- Before serial: parallel port
	- Was point to point, simplex
	- One line per bit, many wires
	- Generally fast and easy to implement but hard at high speed (all signals need to arrive at the same time )
	- Cumbersome, too many connections
- Serial Port: RS-232
	- Point to point, duplex
	- Long line connections for Data Terminals
	- The time of encoding can be transmitted over telephone cables/can be encoded to transmit as audio
	- Originally many configurations in use, so very under-standardised
		- High voltage (dangerous
		- Data length: 5-9 bits (2 2 + 1 for meta information like control commands) 
		- Parity: none, odd or even (almost no advantage between the two) 
			- USB3 must have compressed irregular data to avoid overusing energy on particular frequency and knocking out communication 
		- Number of Stop bits: 1 or 2 
		- Hardware or software handshake
		- Different connectors
- Serial Port UART/USART
	- Most microcontrollers will have a hardware block/blocks specifically made for serial communication
	- UART - Universal Asynchronous Receiver/Transmitter
		- Async requires good quality clocks on both receiver 
		- USART - Universal Synchronous/Asynchronous Receiver/Transmitter (they have a clock wire)
		- Clock line means you can talk faster (don't just have to rely on clocks being right, <= Mbps)
	- Serial ports are very useful for microcontroller communication
		- configuration has converged to: 8N1
			- 8 bit data, 1 stop bit but no parity
			- No handshake wires, done in software instead
		- High voltage
		- Easy to debug  with terminal emulation (output ACSII messages)
		- Bridges to USB readily available 
		- Connection:
			- GND - GND (ground to ground)
			- TX - RX (transmitter to receiver)
			- RX -TX (vice versa)
			- RX- RX is valid but they have nothing to receive
			- TX - TX could cause a short circuit. DANGEROUS
			![[Pasted image 20260517173827.png]]
		- Clocks are quite accurate, UARTs are more sophisticated so one stop bit and no parity is fine
		- Parity can be checked by UART in hardware but there's not really much that can be done if that's wrong
- Baud Speed
	- Baud bits/s
		- Includes all the protocol overhead
		- CPU clock speed will limit a device's baud rate
		- Not all baud speeds may be equally good for a particular processor (a faster speed could be more reliable, may line up with the crystal clock speed of a processor)
		- Right setup baud rate can be recognised automatically

#### SPI
- Bus for Device to Peripherals 
	- SD card
	- Displays
	- ADC (analogue to digital)
	- Sensors
- High speed 
- Synchronous (so has an extra clock line)
- Simple hardware implementation (shift register)

- Main-Sub (master-slave) architecture
	- Not all nodes have the same rights. One should organise as the main one 
	- Main orchestrates operation
		- drives clock
		- Selects the sub to communicate with
	![[Pasted image 20260517174409.png]]
- Used in SD cards, start with SPI then negotiate higher level protocols

#### I2C (Inter-Integrated Circuit)
- This is a proprietary name (so also known as 2 wire protocol)
	- But it's 3 wires because of ground voltage
- Half duplex
- One data line that can go in either direction
- Up to 5 Mb/s (standard is 100 kb/s)
	- Too many -> two much stress, low voltage and high resistance
	- You'll probably want to go at slower speeds

- Push-Pull Output
	- Not in I2C. Actively pushing/pulling. One thing pushing high and the other pushing down would cause a short circuit
- Open Drain
	- used in I2C. Requires pull-up resistors since one is always down/one is always up
- Bus with pull-up

- Pull up resistors 
	- Make sure you have one on the data line (SDA) and clock line (SCL) 
		- You don;t want to waste power
		- But you don't want to do it slowly (too much resistance/delay)
		- For fast communication:
			- aim for low pull-up resistance
				- Extreme - zero
		- For low power consumption 
			- aim for high pull-up resistance
				- Extreme - infinite
- Clock Stretching
	- Slow devices can lengthen clock cycles to have more time to respond
	- Multiple controllers allowed
	- Clock Synchronisation 
	- Bus arbitration
	- Programming a device to behave as a slave is harder than making it the master:
		- timing is very strict
- System Management Bus
	- Can be understood by I2C devices
	- dynamically assigned addresses
	- packet error checking
	- 35 ms timeout 
	- A bit simpler, also something you can do on I2C
	- Good approach if you're having addressing problems

#### CAN
- CAN Bus 
- CAN and Ethernet are multi-master and realtime - so multiple things that can talk whenever they want.
	- So we need to deal with collisions 
	- Has a fixed priority scheme. We decide beforehand who has a priority out of the masters if multiple talk at the same time 
- Say we have a collision and the connection is damaged, who's there to say there won't be another afterwards
- Solution:
	- Devices have an address. More zeros -> higher priority
	- First thing in a packet is an identifier
	- The zeros of a higher priority device will destroy any ones on a conflicting lower priority device due to the passive pullout
	- Zeros kill the ones
	- When a device realises one of their ones has been killed, they stop talking so the higher priority device takes lead during resending the message
		- If you send a 1 and they send the line low, you know you've been clashing with a higher priority one


# References