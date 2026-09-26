2026-09-24 09:03

Status:

Tags: [[Real-Time Computing and Embedded Systems]]


# Real-Time Embedded Systems

#### Definition
- Any processing system which must respond to externally generated input stimuli within a finite and specified period.
	- correctness depends not only on result but also time it was delivered
	- failure to respond is just as bad as the wrong response
- The computer is a component in a larger engineering system
	- Embedded Computer System

#### Generic Real-Time System
![[Pasted image 20260924090527.png]]

#### Car Example
- Man-machine Interface
	- Input
		- Steering Wheel
		- Dashboard Switches
	- Output
		- Speedometer
		- Dashboard Lights
	
- Functions
	- Sat Nav
	- Lane assist
	- Anti-Lock Brakes
- Control Interface
	- Sensors
		- GPS
		- Petrol Gauge
		- Road Cameras
	- Actuators
		- Spark-Plugs
		- Airbag Detonator

#### Contemporary Real-Time System
![[Pasted image 20260924091720.png]]

#### Functional Requirements for Real-Time Systems
- Data Collection
	- A significant state variable is called a real-time (RT) entity
		- e.g. Ignition key or GPS (important stuff))
	- Requirement:
		- Observe RT entities
		- Collect observations to build RT image
	- Different observations (fuel, wheels, brakes):
		![[Pasted image 20260924092355.png]]
- Direct Digital Control
	- Calculating the "set points" for actuators and controlling the objects
		![[Pasted image 20260924092341.png]]
	- Mostly out of scope
		- If we need a control algorithm in this course, it will be stated for us or given to us.
- Man-Machine Interaction
	- An RT system must inform the operator of the current state of the controlled object and assist in controlling the machine
		- Feedback must be clear and unambiguous 
		- Risk of user error must be minimised
	- Also mostly out of scope

#### Non-Functional Requirements for Real-Time Systems
- Functional: what the system should do
- Non-Functional: what the system should be
- Temporal requirements:
	- Minimal Latency Jitter
	- Minimal Error-Detection Latency
- Qualities
	- Reliability
	- Safety
	- Maintainability
	- Availability
	- Security

#### Temporal Requirements 
![[Pasted image 20260924093644.png]]

- Timing Relationships
	![[Pasted image 20260925145902.png]]

#### Real-Time System: A Car
![[Pasted image 20260925150228.png]]


#### Practical d_sample and d_computer
![[Pasted image 20260925150805.png]]

Should become:
![[Pasted image 20260925150838.png]]

So d_computer < d_sample
# References