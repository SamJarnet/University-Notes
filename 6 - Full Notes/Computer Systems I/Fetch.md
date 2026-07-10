09-10-2024 16:59

Status:

Tags: [[Computer Systems I]] [[CPU]] [[FDE Cycle]]

# Fetch

#### Fetch process:
- PC contains address of next instruction
- Address moved to MAR
- Address placed on address bus
- CU requests memory read
- Result placed on data bus, copied to MBR, then to IR
- Meanwhile the PC is incremented by 1 (With 32-bit instructions the PC increments by 4 bytes after each instruction)

# References