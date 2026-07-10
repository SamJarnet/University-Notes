03-10-2024 16:22

Status:

Tags: [[Computer Systems I]]


# ADC chip

#### How does it work?
- All ADC use one or more comparators, which compare two analogue inputs and produce a digital output depending on which is higher
- Can sense anything with appropriate transducer
- The simplest system to understand is the probably one that is not often used: the flash ADC
#### Flash ADC:
###### Simplified Flash ADC:
 ![[Pasted image 20241024151454.png|400]]
- Very fast, but expensive
#### Specs:
- 10 bit ADC (1024 levels)
- 8 channels - or inputs
- It connects to the [[Raspberry Pi]] using the [[SPI Bus]] bus
- [[Python]] uses a library which transfers data from the ADC over an [[SPI Bus]] bus


# References