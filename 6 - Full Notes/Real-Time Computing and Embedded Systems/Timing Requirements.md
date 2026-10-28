2026-10-20 10:06

Status:

Tags: [[Real-Time Computing and Embedded Systems]]


# Timing Requirements

#### Safe Timing Behaviour
- Requirements
	- Focus on what should be done, avoid assumptions about how
	- Individual requirements are often formulated as a stimulus and a response, related to aspects of the environment. Alongside a timing requirement

#### Where do the timing requirements come from?
- Most common timing requirement:
	- React to an external event within $x$ time units
	- Also known as response-time requirement or a deadline requirement
- An internal system event is like a detection and an external one like the outcome (e.g. a crash)

#### Mixing Internal and External events
- Functions with response time requirements are often implemented by periodic activities
- We must distinguish between requirements and design, that is, between:
	- timing constraints at the external system level
		![[Pasted image 20261026164822.png]]
	- timing properties of individual design units
		![[Pasted image 20261026164851.png]]

