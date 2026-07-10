09-10-2024 16:54

Status:

Tags: [[Computer Systems I]]


# CPU

#### Functions of the CPU:
- Data processing 
- Data storage
- Data movement
- Control

#### Instructions:
- CPU families have different instruction sets
- So x86, ARM, MIPS, Risc V, etc can not run each others machine code
- We usually write high level code and compile it for specific architecture

#### The CPU must:
- [[Fetch]] instructions
- Decode/Interpret instructions
- [[Execute]] instructions
- [[Fetch]] data
- Process data
- Write data
- Run [[Interrupts]]

#### CPU Clock:
- Drives the steps in the processor
- Systems are synchronous - i.e. everything happens on the clock edge
- 1 GHz is a nanosecond

#### Special purpose registers:
- Program Counter (PC) - Contains the address of an instruction to be fetched
- Instruction register (IR) - Contains the most recently fetched instruction
- Memory address register (MAR) - Contains the address of a location in memory
- Memory buffer register (MBR) - Contains a word of data to be written to memory or the word most recently read

#### Instruction set:
- Could be [[CISC]] or [[RISC]]
- Runtime = instruction-time X cycles-per-instruction X Ninstruction
- CISC tried to reduce Ninstruction
- RISC tried to reduce cycles-per-instruction
# References