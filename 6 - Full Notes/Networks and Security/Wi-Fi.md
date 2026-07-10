04-04-2025 16:22

Status:

Tags: [[Networks and Security]]


# Wi-Fi

#### What is Wi-Fi?
- Wi-Fi (Wireless Fidelity) is essentially the wireless alternative to Ethernet
	![[Pasted image 20250404162427.png]]

#### How does it work?
- Wireless network with an access point (AP)
- AP that connects to the wired network
- AP transmits radio signals in a specific frequency range (2.4 GHz or 5 GHz)
- Client devices associate with the AP and receive these signals 
- Service Set Identifier (SSID) to identify a network

- Ad hoc network (used much less often): clients connect directly without AP

#### 2.4 Ghz vs 5 Ghz:
- 
	![[Pasted image 20250404162751.png]]

#### The IEEE 802.11 Standard:
- Uses the IEEE 802.11 suite of protocols. Has evolved over many years (802.11b, 802.11a, 802.11n, ...)
	![[Pasted image 20250404162912.png]]
- Theoretical maximum speeds ^

#### Wi-Fi Performance:
- IEEE 802.11 standards define maximum theoretical speeds, actual speeds are lower in practice
- Factors affecting Wi-Fi performance: signal strength, interference, network congestion
- Techniques to enhance performance: MIMO, beamforming, channel bonding, quality of service

#### Wireless Network Challenges:
- Ethernet:
	- Devices receives every other node's transmissions (e.g. hidden node)
	- Devices can transmit and receive at the same time 
- Wi-Fi:
	- Rely on shared communication channels
	- Devices can't always sense each other's transmissions
	- Devices can't transmit and receive at the same time

#### Hidden Node:
- A situation where two devices can't detect each other's signals but are both communicating with the same access point, leading to collisions
	![[Pasted image 20250407181639.png]]

#### Solution for hidden node:
- Request to Send / Clear to Send (RTS/CTS):
	- Device A sends an RTS (Request to Send) to the access point
	- The access point replies with CTS (Clear to Send) if the channel is free
	- Device A transmits data, while other devices wait

#### What is CSMA/CA?
- In wired networks: CSMA/CD (Collision Detection)
- In wireless networks: CSMA/CD doesn't work well because devices can't always detect collisions. 
	- Wireless networks use CSMA/CA
- CSMA/CD: Listens to the channel, transmits and if a collision is detected, it stops, waits and retransmits
- CSMA/CA: Listens to the channel and waits for it to be idle before transmitting; uses ACKs to confirm receipt

#### How does CSMA/CA work?
- 1. Carrier Sense (listen before transmitting)
- 2. If busy, it waits (backoff time)
- 3. If free, it sends the data.
- 4. Request to Send (RTS) and Clear to Send (CTS)
- 5. Acknowledgement (ACK)

#### Exposed node:
- A situation where a device incorrectly assumes the channel is busy and unnecessarily delays transmission.
	![[Pasted image 20250407183227.png]]

#### Future trends in Wi-Fi:
- Emerging technologies: Wi-Fi 7 and beyond
- Increased user of the 6 GHz Band
- The role of Wi-Fi in the Internet of Things (IoT)

#### Summary 
- Wi-Fi enables wireless internet access using radio waves. 
- Collision avoidance with CSMA/CA.
# References