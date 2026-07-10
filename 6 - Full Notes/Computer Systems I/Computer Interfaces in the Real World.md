22-12-2024 14:34

Status:

Tags: [[Computer Systems I]] [[Computer Interfaces]]


# Computer Interfaces in the Real World

#### System - block diagram:

![[Pasted image 20241222143454.png]]

#### Input examples:
- Sound, temperature, touch, motion, light etc.

#### Possible system inputs:
- binary, read as "0" or "1", buttons and switches, debouncing problems
- Many inputs will be analogue
- typically read by a transducer or a sensor
- they may have digital outputs, but have internal conversion to digital

#### Transducer input:

![[Pasted image 20241222143909.png]]


#### Temperature as an example:
- range (in UK):
	- -20 degrees C to +35 degrees C
- continuous (infinite precision)
- convert to digit (e.g. 12 bit conversion)

#### Quantisation:

![[Pasted image 20241222144316.png]]

Digital conversion introduces "steps"
#### Scaling/amplifying:
- Input to ADC could be limited (e.g. 1.8V)
- Signal may be small - so an amplifier is needed
- e.g. small signal from 0V to +1V
- This would be read as 0 to 4096 * 1/1.8 = 2275
- Each step would be 1/2275 volts
	- Ok but loses precision so an amplifier with gain of 1.8 could be used
- Small signals need amplification – e.g. microphones

#### Shifting/offset:
- Signal may be negative e.g. -1 to +1V
	- So shifting the input up 1V would be needed
	- That could make the maximum > 1.8V
- In practice signal is shifted "up" so 0 = -1V and 4096 = 1V (example of a 12 bit ADC)

#### [[ADC chip]]: 
- Can sense anything with appropriate transducer (an electronic device that converts energy from one form to another. Common examples include microphones, loudspeakers, thermometers, position and pressure sensors, and antenna.)
- design decisions:
	- number of bits (usually 8,12 common, 16 also possible)
	- speed of conversion (time before a change in the input voltages is reflected in a change in the digital output)
	- cost

#### How does an ADC work?
- All ADC use one or more comparators, which compare two analogue inputs and produce a digital output depending on which is higher
- Can sense anything with appropriate transducer
- The simplest system to understand is the probably one that is not often used: the flash ADC

- ![[Pasted image 20241222145056.png]]

#### Simplified flash ADC:
- Triangle comparators output High if + is higher than -
- Each one compares Vin to a voltage
- Highest D sets the 3 bit output

- ![[Pasted image 20241222145155.png]]

#### The flash ADC:
- Very fast, but expensive
- one comparator for every quantised voltage level (i.e. an 8-bit ADC will contain 256 comparators, each producing a digital output)
- the 256 outputs can be quickly encoded into the required 8 bit digital output 
- Fast enough to sample at GHz rates for radar etc.

#### Range and quantisation 
- If Full Scale Range is 3.3V each ADC step is 3.3/4096 = 0.0008V or 0.8 millivolts (mV) 
- In practice it depends on the settings used and the ADC may use a “Reference Voltage”
- For AC signals (e.g. microphones) 0V will be set in the middle of the range


#### MCP3008 
- In labs we use the MCP3008 ADC 
- Successive approximation ADC 
- 10 bit resolution 
- 200 kHz max sample rate 
- Accuracy is expressed like 
	- ±1.5 LSB offset error, ±1 LSB gain error 

- Digital value = 1024 * Vin/3.3 
- When used with a 3.3V power supply like we do

#### The Digital to Analogue Converter (DAC):
- Takes a digital input and converts it to an analogue voltage
- Same precision/quantisation issues as with the ADC:
	- e.g. a 5 volt 8 bit DAC will change in "steps" of about 20 mV
- Same cost/speed issues as with the ADC (but always fast than an ADC, except maybe the flash ADC)

#### Sampling rate:
- how fast should you sample the analogue signal?
- Look what happens to our red signal if we sample too slowly: aliasing

![[Pasted image 20241222150013.png]]


#### Sampling:
- You need to sample at least as fast as the Nyquist rate:
	- 2 times the highest frequency in the signal
- e.g. sounds up to 20KHz need min 40KHz
- Otherwise you get aliasing/moire
- If you can't - you have to filter out all of the frequencies above sampling rate/2

#### Aliasing in images:
- if you sample an image you can get aliasing too! e.g. shrinking an image badly with “high frequency” detail

![[Pasted image 20241222150333.png]]

#### DAC conversion:
- Perfect reproduction of analogue signal is not normally possible:

- ![[Pasted image 20241222150443.png]]

#### Analogue Outputs:
- Sound - to speakers
- Voltage to control motors/actuators
- Historically: RGB signals to analogue monitors (e.g. VGA)

#### PWM 
- Pulse Width Modulation 
- Is an on/off signal often used for motors or LEDs 
- e.g. the more ON the brighter the LED or the faster the motor turns 
- Microcontrollers usually have PWM hardware to make these signals

- ![[Pasted image 20241222150649.png]]

Summary 
- introduction to DAC, ADC and real-world inputs/outputs 
- Introduction to sampling 
# References
