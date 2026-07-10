22-04-2025 16:03

Status:

Tags: [[Networks and Security]] [[Link Layer]] [[Application Layer Protocols]] [[Network Layer]]


# Link Layer

#### Reference:
![[Pasted image 20250422160524.png]]

#### Layer encapsulation:
- Each layer adds it's own header
- This becomes part of the payload for the layer below it
	![[Pasted image 20250422160617.png]]

#### Link Layer shields upper layers from specific connection type:
![[Pasted image 20250422160648.png]]

#### Media types in the Physical Layer:
- There are a wide range of physical media types
- We need standards for transmission of bits on each media type, which can be used by the link layer e.g. Coaxial cable, twisted pair,  power line, fibre optic, wireless, laser, sound, pulses, ...
- e.g. IEEE802.11 standards define transmissions for [[Wi-Fi]]

#### Transmitting bits:
- Bits are transmitted using encoding schemes, e.g. Manchester encoding, 8b/10b, etc.
- Transmissions is based on varying something over time, typically based on voltage or frequency, with synchronisation

#### Link Layer functions: 
- Transmission of frames over physical media
	- Encapsulates IP datagrams into Link layer frames
- Receives frames, passing IP datagrams up the stack
- Detection and handling of transmission errors

#### Packets and frames: 
![[Pasted image 20250422161233.png]]

#### Link-Layer can vary end to end:
- Each section might have its own physical and link layer
	![[Pasted image 20250422161640.png]]

#### Data Frames:
- Frames vary depending on the physical layer e.g. [[Ethernet]] frame:
	![[Pasted image 20250422161904.png]]

#### Flow control:
- May regulate flow of data - So a slow receiver is not swamped by a fast sender
- Can use messages to sender saying more data can be sent
- Can be rate-based so the speed is agreed
	- Rarely used in this lower layer

#### Link Layer Acknowledgements:
- Three general link layer models may be used:
	- Connectionless, no acknowledgements
		- For low error rate networks, e.g. wired Ethernet
		- It's "connectionless" in that no signalling path is established in advance
			- The frames are sent, and may or may not be received by the destination
	- Acknowledged, connectionless service
		- e.g. wireless 802.11 Wi-Fi
		- 802.11n supports block acknowledgements
	- Acknowledged, connection-oriented services
		- For long delay, or unreliable links, e.g. satellite

#### Handling ACKs and errors
- Different strategies/protocols available
- Simplest to Stop-and-Wait Automatic Repeat reQuest (ARQ)
	- Send a frame, wait for ACK, send next frame, etc
	- Will not get an ACK if frame is lost or damaged
- Can improve this by pipelining
	- Send multiple frames before receiving the first ACK
	- Go-back-N ARQ
		- Uses a sequence number to label each frame
		- Send many frames; if an ACK is missed, retransmit from that frame
	- Selective-Repeat ARQ
		- Similar, but only retransmit lost frames

#### Error detection/correction:
- Can provide a line "free of errors" to the network layer
	- Requires error or packet loss detection and subsequent retransmission 
	- Upper layers may have their own error detection methods
	- No radio-link is 100% error free!

#### Detecting errors:
- Simplest method is parity bit
	- Is number of 1's even or odd (e.g. 10101011 even-parity 1)
	- Clearly will not reveal all errors
- We require a more robust method:
	- Example: CRC: Cyclic Redundancy Check
	- Result is held in the "checksum" field of the frame
	- Calculated by sender and receiver, and results compared

- Checksums may happen at other layers too
	- IPv4 has a checksum, IPv6 does not

#### Framing:
- Each sequence of link layer bits needs to be framed
	- To indicate where the frame starts and ends
	- For example, to form an Ethernet frame
	- uses some bandwidth to indicate the start/end of frames
- Various approaches:
- e.g. Use a FLAG byte value to mark the start and end
	- If FLAG occurs in the actual data, use and Escape byte
	- When receiving, string (ignore) first Escape byte
	- If an Escape byte occurs in the data, Escape that

#### MAC - Media Access Control:
- A MAC protocol manages access to/from the PHYS medium
- It is part of the link layer
- It has a mechanism for sending frames to/from PHYS and typically manages channels/frequencies/collisions
- Typically very specific to a type of PHYS layer
- PHYS may need extra bits added to frame

#### Link Layer example: Ethernet:
- Twisted pair cable with switches
- Packet switched 
	- One device per switch port
	- Campus has 1Gbit/s to the desk and 10Gbit/s backbones
	- No contention over a medium if switch has sufficient internal bandwidth

#### Link Layer example: Wi-Fi:
- Wi-Fi is basically a wireless alternative to Ethernet
	- Uses the IEEE 802.11 suite of protocols
	- Works in 2.4GHz or 5GHz range (also new 6GHz and 60GHz)
- Has evolved over many years
- Devices associate with a wireless Access Points (AP)
- Shared media, so significant contention in busy areas
	- Therefore uses a collision avoidance scheme

#### Handling media contention:
- Original Wired Ethernet - used Carrier Sense Multiple Access with Collision Detection (CSMA/CD)
- Something is needed when using a single, shared media to ensure only one sender is transmitting at any time
	- Less important in modern fully-duplex switched Ethernet networks
	- More important on a radio network

#### CSMA/CD operation:
- Works a little like a telephone conversation
- Sender listens to see if the media is busy
	- If it is it waits
- When channel is free, the sender starts to talk
	- Listen while sending and stop if collision occurs
- Back off before retransmitting if collision detected
	- Pick the back off delay from an increasing set of values

#### Wi-Fi and collision avoidance:
- Wi-Fi doesn't use CSMA/CD because Wi-Fi devices can't generally send and receive at the same time
	- There is also the "hidden node" problem - devices see AP but not each other
	- Instead they use CSMA/CA (CSMA/Collision Avoidance)
- CSMA/CA is like CSMA/CD but instead of listening into the transmission, it waits for an acknowledgement from the AP to determine if the frame was successfully sent. Faster 802.11n allows block acknowledgements.
- Can also optionally use Request to Send / Clear to Send (RTS/CTS) signalling to the AP to improve performance
# References