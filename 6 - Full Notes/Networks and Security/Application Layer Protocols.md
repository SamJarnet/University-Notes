28-02-2025 09:05

Status:

Tags: [[Networks and Security]] 


# Application Layer Protocols

#### DHCP (Dynamic Host Configuration Protocol):
- Protocol to automatically assign IP addresses to devices on a network
- Dynamic assignment:
	- Devices request an IP address from the DHCP server
	- The server leases an available IP address for a specific period (lease time)
	- Once the lease expires, the IP address may be renewed or reassigned
- Advantages:
	- Automated IP assignment: No need for manual configuration
	- Efficient IP management: Ensures devices get unique IPs


#### SMTP (Simple Mail Transfer Protocol):
- Reliable protocol to send emails. Responsible for sending but not receiving emails
- 1. Client to Server: Sender's email client connects to the SMTP server and sends the message
- 2. Server Relay: SMTP server checks the recipient's domain and locates the correct mail server
- 3. SMTP Transfer: Sender's SMTP server connects to the recipient's SMTP server and transfers the email
- Final Delivery: Recipient's SMTP server stores the email until retrieved via IMAP or POP3






- Text-based protocol that uses specific commands and responses
- SMTP Authentication is an extension:
	- Original email had none so mail relays were used for spam

	![[Pasted image 20250228091006.png]]



#### IMAP (Internet Message Access Protocol):
- Protocol used by email clients to retrieve and manage emails stored on an email server
- 1. Connection to Mail Server: ports 143 (standard) or 993 (for encrypted connections)
- 2. Email Synchronisation: Client keeps a TCP connection open to send requests or receive notifications
 - Unlike POP3 (Post Office Protocol 3), it keeps emails on the server

#### Hypertext Transfer Protocol (HTTP):
- Used for web browsing and communication between web servers and clients
- 1. The browser connects to the web server using TCP (normally) on port 80 or port 443 for HTTPS
- 2. The browser sends a request to the server using methods like GET /something/page.html HTTP/1.1
- 3. The server responds with an HTTP status code (e.g. 200 OK for success or 404 Not Found if the page doesn't exist) and the requested content
- 4. The browser processes the response and displays the webpage, fetching additional recourses like images and stylesheets

#### The main HTTP requests:
- Text based protocol
- GET: Request a webpage or resource
- HEAD: like GET but no data is sent back
- POST: send data to the server, could create
- PUT: update resource on the server
- DELETE: remove a resource

#### Typical Response:
- HTTP/1.1 200 OK
- Date: Mon, 21 Nov 2017 09:38:34 GMT
- Content-Type: text/html; charset=UTF-8
- Content-Encoding: UTF-8
- Content-Length: 138 
- Last-Modified: Wed, 08 Jan 2012 23:11:55 GMT
- Server: Apache/1.3.3.7 (Unix) (Red-Hat/Linux)
- ETag: "3f80f-1b6-3e1cb03b" 
- Accept-Ranges: bytes 
- Connection: close 
- Followed by the payload

#### Status Codes:
- 1xx -> Information
- 2xx -> Success
- 3xx -> Redirection (e.g. 301 Resource moved to a new URL)
- 4xx -> Client error (e.g. 403 access forbidden, 404 not found)
- 5xx -> Server error (e.g. 500 internal error)


#### HTTPS: 
- HTTP provides no security guarantees 
- HTTPS wraps HTTP in a TLS session to achieve confidentiality and integrity

#### HTTP/2 and HTTP/3:
- version 2:
	- First major revision to HTTP, published in 2015
	- Header compression
	- Multiplexing multiple requests over a single TCP connection
- version 3:
	- Does not use TCP connections like HTTP1 and 2 but runs over QUIC

#### Constrained Application Protocol:
- CoAP provides lightweight HTTP-like protocol for simpler devices
	- Minimal overhead. Good for IoT
	- Uses UDP instead of TCP for faster communication
	- Similar to HTTP (supports GET, POST, PUT, DELETE)
- CoAPs used in IKEA smart lighting for example 

#### QUIC (Quick UDP Internet Connections):
- New transport protocol designed to replace TCP (Transmission Control Protocol) in specific situations
- Built on top of UDP
	![[Pasted image 20250228093030.png]]

- Real-time communication (e.g. video conferencing, gaming)
- Streaming (video/audio with minimal buffering)
- Its adoption is expanding, with major tech companies like Google and Cloudflare

#### RTSP (Real Time Streaming Protocol)
- Network protocol designed for streaming media (e.g. video or audio) over the internet
- Controls playback of audio/video streams: SETUP, PLAY, PAUSE, TEARDOWN
- Has a URL Scheme with arguments
- rtsp://catvideos.org/media#t=10

#### RTP (Real-Time Transport Protocol):
- Handles the actual transmission of real-time media (video, voice)
- It runs over UDP for low latency (faster than TCP)
- Uses sequence numbers to detect lost packets
- Includes timestamps to synchronise audio and video












# References