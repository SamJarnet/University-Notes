27-12-2024 22:11

Status:

Tags: [[Computer Systems I]] 


# Microcontrollers

#### What is a Microcontroller?
- A self-contained computer on a single chip
- 8 bit and 16 bit used to be common, 32 bit now king
- Slow clock: typically 32kHz to ~100 MHz
- Small [[RAM]], small storage and can be very low power
- Very cheap - billions per year, > 55% of all [[CPU]]s sold

#### Memory:
- Registers
- SRAM: as low as 1k
- Flash/EEPROM:
	- 16-64k for programs
- Typically no cache
- Microcontrollers generally don't have a Memory Management Unit (MMU)

#### No MMU?
- "Normal" computers hide physical memory from processes using virtual memory management
	- Enabled paging, segmentation, etc.
	- Hides fragmentation
- Needs hardware support: an MMU:
	- Translates virtual addresses to physical addresses
- Microcontrollers can't run a "real" operating system

#### Input/Output:
- Generally have:
	- General purpose I/O
		- Interrupts
		- Pulse Width Modulation (PWM)
	- Timers, clocks, counters
	- Serial interfaces
		- USART, UART, SPI. I$^2$C, CAN
- Could also have:
	- ADCs and DACs for Analogue I/O
	- Capacitive touch interfaces
	- Networks, screen interfaces, USB interfaces, etc.


#### Low Power:
- Commonly designed for battery use:
	- Hundreds of $\micro$A in stand-by/sleep
- Microcontroller: $\micro$W or mW
	- Modern CPU: ~ 2-280 W

#### Microprocessor vs Microcontroller:
- Microprocessor:
	- CPU, RAM, storage, I/O, timer, etc. are typically seperate
	- Amount of RAM, storage and I/O can be set at design time
	- Higher cost, but more versatile and general-purpose
	- High performance
	- High power
	- 64-bit is common
	- Typically a deep pipeline
- Microcontroller:
	- Everything integrated into a single chip
	- Fixed amount of on-chip RAM, storage and I/O
	- Low cost for applications that are space and/or power constrained
	- Low performance
	- Low power
	- 8, 16 and 32-bit are common
	- Shorter pipeline 


#### Where are Microcontrollers used? 
 - Smart devices 
 - Vending machines 
 - Computer peripherals 
 - Industrial, aero and space 
 - Embedded controllers in other devices

#### Range of examples:
- Some use Harvard architecture, some use Von Neumann and some a mix of both
- Range of bandwidth

#### Programming Microcontrollers:
- Microcontrollers need to be programmed
- We will look at a few ways of doing it, and use LED flash as an example

#### Bare-Metal Programming:
- Commonly "bare-metal" programming with no OS:
	- Write code in C
	- Compile
	- Flash to microcontroller
- Unlike desktop applications, efficiency and memory usage are much more of a concern

#### Embedded OS
- We can't Linux of Windows on a microcontroller BUT embedded operating system do exist
- $\micro$Clinux
- Real-time operating systems:
	- FreeRTOS, $\micro$C/OS/Mbed OS 
- IoT operating systems
	- RIOT-OS, Contiki-NG, TinyOS

#### The Arduino Platform:
- [[Open source]] hardware and software:
	- IDE for writing C++
	- Libraries for interacting with hardware
- A range of platforms where code can be moved from platform to platform
	- Originally developed with the Arduino Uno
	- Now includes devices with a range of microcontrollers

#### MBED:
- Cloud-based IDE and OS for ARM-based microcontrollers
- Code is written in C in a web-based IDE and compiled on a remote server
- Binary dropped onto a mounted flash "drive" to program

#### MicroPython: 
- A cut-down version of Python 3 for microcontrollers
- Python compiler to bytecode and a runtime interpreter 
- Read-eval-print loop
	- Presents a Python shell over serial
	- Code is interpreted rather than compiled
- Needs 16kB of RAM and 256kB of flash

#### The Problem with Embedded OS and Libraries 
- Licensing…

#### System-on-Chip:
- Conceptually similar to a microcontroller
- Integrates most of the components of a computer in a single chip
- Microcontroller SoC usually include radio, co-processors, interface drivers, etc.
- Microprocessor SoC usually include CPU, I/O devices, memory (possible soldered on top...), graphics card, network, etc.


#### Microcontroller SoC with a radio:
- Microcontroller with a radio in the same package.
- Useful for IoT applications

#### Microprocessor SoC:
- Includes processor, graphics, networking and may include RAM
	- RAM could be Package-on-package
- Common in phones embedded (e.g. Raspberry Pi) and network equipment
- Starting to appear more in laptops




# References                    