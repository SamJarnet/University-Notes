
24-10-2024 15:04

Status:

Tags: [[Computer Systems I]] [[ADC chip]]


# Computer Interfaces

#### Possible system inputs?
- some will be "binary"
	- e.g. switches, buttons - read as 0 and 1
	- still potential problems like debouncing
- many will be analogue
- typically read by a transducer or sensor
- they have digital outputs, but have internal conversion to digital

#### Scaling/amplifying:
- Input to ADC could be limited (e.g. to 1.8V)
- Signal may be small - so an amplifier is needed
- e.g. small signal from 0V to +1V
- This would be read as 0 4096x1/1.8 = 2275
- Each step would be 1/2275 volts
	- this loses some precision as an amplifier with gain of 1.8 could be used
- Small signals need amplification - e.g. microphones

#### Shifting/offset:
- Signal may be negative e.g. -1V to +1V
	- So shifting the input up 1V would be needed
	- This would make the maximum > 1.8V 
- In practice signal is shifted "up" so
	- 0 = -1V
	- 4096 = 1V (example for a 12 bit [[ADC chip]])


[[Computer Interfaces in the Real World]]

# References 