10-03-2025 15:13

Status:

Tags: [[Networks and Security]]


# Transport Layer

#### Layer:
- The layer above the [[Network Layer]]:
	- Sends segments (or datagrams via the Network Layer)
	- Passes a received packet's payload to the (correct) Application
- Provides host-unique port numbers
- Provides logical communication between applications

#### Another view:
- TCP or UDP are the main transport protocols
- The IP packet protocol field in the header specifies which
	![[Pasted image 20250310151725.png]]

#### Transport Layer Addressing
- Both TCP and UDP use 16-bit port numbers 0-65535
- Uniquely identifies a connection endpoint on the host
- Conventions surround port allocation:
	- Port 0: TCP Reserved, UDP "No Port"
	- 0-1023: Well-known ports
	- 1024-49151: Registered ports
	- 49151-65535: dynamic/private ports
- Official list of well-known and registered ports maintained by IANA

#### TCP: Transmission Control Protocol:
- Connection oriented
- Includes acknowledgements and retransmissions
- Provides flow control/congestion control for segments it sends
- TCP will adjust sending rate over time

#### TCP:
- Properties of TCP
	- Provides connection management
		- Similar to the concepts we briefly looked at for the link layer
	- Provides flow control
	- Uses that capacity but tries to also avoid congestion
	- Retransmission 
	- Receiver reassembles segments in the correct order
- So TCP provides performance and reliability on an otherwise unreliable IP service

#### TCP Header:
![[Pasted image 20250310152733.png]]

#### TCP connection establishment
- Three way handshake:
	- SYN, SYN-ACK, ACK
	 ![[Pasted image 20250407183658.png]]
	- SYN opens connection (with random seq num)
	- Server ACKs 
	- Client ACKs
	- Connection is now established 
- Each side uses a sequence number
	- Repeat packets can be discarded, lost ones re-sent
	- Common understanding of position in data stream

#### TCP Reliability:
- ACKs are sent back by receiver
- Sender must detect lost packets
	- By Retransmission timeout
		- Estimate when ACK is expected

#### UDP: User Datagram Protocol:
- Connectionless, "Send and Forget"
- Retransmission/adaptation is up to the application 
- No flow control; UDP applications are often fixed bit rate

#### UDP:
- Properties: 
	- Connectionless
		- Sender just sends a datagram to a receiver
		- No sequence numbers, no acknowledgements
	- If retransmission is required, the application has to do it - so it is up to the application layer
		- It may or may not be necessary to resend
	- Some UDP applications may use a constant bit rate
		- e.g. video streaming, up to application to adapt if necessary
	- Low overhead:
		- Because no connection management being used 
		- Uses less bandwidth for the UDP header

- Allows sending of datagrams without establishing a connection
- The UDP header is much simpler that TCP
- Checksum is optional
- Can multicast (one-to-many)
	![[Pasted image 20250407195902.png]]


#### UDP loss:
- Lossy/congested links can drop packets
	- Higher protocols can send a request back to source if needed
- Lower bandwidth links may drop packets as their buffers fill up
	- Applications could detect this and tell server

#### TCP/UDP service model:
- Sender and receiver each create a socket to act as a communication endpoint
- Socket has IP address and port number
- Need five bits of information to identify communication 

- The sockets and protocol used, uniquely identify the application's subsequent data transmissions
- Many ports are reserved for specific protocols 

#### Multiple clients:
- Multiple clients communicate with the same server
	- Each client endpoint will be different
	- Server multiplexes connection, e.g. 1 thread per client endpoint 

#### Berkeley Sockets API:
- Example of an API to use sockets (C)
	- Server-side: socket() and bind()
	- Client-side: socket() and connect()
	 ![[Pasted image 20250407202015.png]]

#### TCP Flow/Congestion Control:
- Flow Control (a):
	- Prevents a fast sender overwhelming a slow receiver
- Congestion Control (b):
	- Reduces send rate to cope with network congestion

#### TCP Flow Control:
- TCP uses a sliding window protocol to control the sending rate
	- Receiver has limited incoming buffer size
- Sender should not send data unless receiver indicates it has buffer space to accept it
	- Otherwise will only have to resend later 
	- And wastes network bandwidth
- The "sliding window" is effectively the buffer space the receiver says it has available at any given time
	- This will change over time 

- The sender sends a segment with a sequence number and starts a timer 
- Receiver replies with an acknowledgement number showing next sequence number it expects to receive and its available window size
	- If receiver says window size is 0, the sender may send a 1-byte probe to get a new window advertisement
		- Or wait until receiver indicates it has capacity
	- Best seen as a diagram
	![[Pasted image 20250407203246.png]]

#### TCP Congestion Control
- Maintained by the sender
- The TCP congestion window indicates the number of bytes a sender may put into the network at any time
	- Packet loss is a signal of congestion
	- Runs alongside the receiver's sliding window
	- Use the smaller of the two windows when sending
- The congestion window size starts low
	- Add one segment's worth per segment acknowledged before acknowledgement timer goes off
	- Known as "slow start"
	- If successful, this doubles the window every round trip
	![[Pasted image 20250411170618.png]]

#### Video: TCP or UDP?
- TCP for video
	- The solution used by YouTube, for example
	- Commonly called "web streaming"
	- Client connect via TCP (http) and receives the video data, buffering it before playback
	- On a fast link, the client can typically buffer ahead if watching pre-recorded video
	- Problematic if link capacity not enough, and TCP backs off - you may see the "hourglass of doom"
		- Will stop playing rather than play "broken" video
	- Not so well-suited for live vide
- UDP is faster but packet loss has to be handled by App

#### Popular use of UDP:
- Video/audio
	- Streaming clients such as VideoLAN (vlc)
	- Immediate, limited buffering, no retransmission
		- Usually fixed transmission rate, e.g. perhaps 5Mbit/s for a given type of higher quality video encoding
	- May experience "glitches" in the video, rather than video hanging, in the event of congestion
	- Well-suited to live video or voice of IP
		- Especially for low UDP head overhead with VoIP
	- Can be used in the newer HTTP/3 standard
	- Very well-suited for multicast

#### DNS: TCP or UDP?
- DNS provides a fairly lightweight lookup service:
	- Client asks a single query
	- DNS server gives an answer
	![[Pasted image 20250411171605.png]]

# References