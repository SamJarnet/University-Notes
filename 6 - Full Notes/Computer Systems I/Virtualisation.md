28-12-2024 13:32

Status:

Tags: [[Computer Systems I]]


# Virtualisation


#### Normal [[Operating Systems]] model:
- All applications access hardware resources via system calls to OS
- Advantages:
	- Design is decoupled between hardware and development and OS development
	- Hardware and software can be upgraded without notifying the application program
- Disadvantages:
	- Applications compiled on one Instruction Set Architecture (ISA) will not run on another ISA
	- ISA must support old software
	- Software not necessarily optimised for hardware

#### Traditional vs Virtualisation:
- Virtual Software placed between hardware and conventional software (e.g. Hypervisor)
- Virilisation involve emulating the hardware
	- Mapping of virtual resources ([[CPU]], [[Registers]], [[RAM]])

#### What needs emulation?
- CPU and Memory
- Registers State, Memory state
- MMU
- page tables, segments
- Platform
- Interrupt controller, timer, buses
- BIOS
- Peripheral devices
- Disk, network interface, serial line

#### Virtual Machine Monitor (VMM):
- A layer of software emulating hardware of a complete computer system
- Provide an abstraction called VM
- Could provide a VM identical hardware to underlay hardware platform (can be other emulated hardware)
- VMM provides the illusion of multiple machines on a single physical machine
- VMM provides means of isolation that untrusted applications run separately
- Even memory management is seperate

#### Binary translation:
- Translate all of the code to new code needed for the VM
- Detect all sensitive/privileged instructions 

#### Paravirtualization:
- Change the guest OS so that it cooperates with the VMM 
	- CPU paravirtualization
	- MMU paravirtualization
	- I/O paravirtualization
- VMM exposes hypercalls for:
	- activate/deactivate the interrupts
	- changing page tables
	- accessing virtualised peripherals
- VMM uses events to trigger interrupts in the VM

#### Hardware assisted virtualisation - x86:
- Allows the VMM to run privileged code:
	- It gets caught and passed to the hypervisor
	- Doesn't need to be translated
	- So it's faster!
- VT-x standard in CPUs is for VMs

#### Hardware assisted Virtualisation:
- VM entry:
	- New instruction that switches the CPU in non-root mode
	- The processor state is loaded from the guest state of the VM Scheduled to run
	- The control transferred from VMM to the VM
- VM Exit:
	- Saves the processor state in the guest state area of the running VM
	- Loads the processor state from the host-state area
	- Transfers control to the VMM


#### QEMU:
- Uses binary translations via Tiny code Generator for efficient emulation
- Supports multiple CPU architectures:
	- ARM, x86 on x86 CPU
	- Hardware emulation
		- Process and system level
		- MMU
		- I/O emulation
- Used with KVM for accelerated virtualisation utilising CPU support


#### KVM:
- [[Linux]] device driver for hardware virtualisation
- VMM components inside the Linux kernel


#### VMware:
- Popular with corporate installations
- Buy a license for each server
	- ~$5000/year per core
	- Workstation Player version is "free" for personal use
- Has good support for large systems
	- Fault tolerance
	- Migrate VMs
	- Backup/snapshots
- Some backlash after Broadcom bought VMware


#### Lightweight containers:
- Instead of having a full OS for each simple service 
- Use the kernel of the host system to run only the code needed 
- Makes it possible to run hundreds of services

#### Cloud:
- Cloud computing depends on virtualisation 
	- Servers
	- Storage
	- Network
	- Application
	- Desktop
	- Shared virtual GPUs
- Leads to:
	- Platform as a service: PaaS
	- Infrastructure as a service: IaaS
	- Software as a service: SaaS

#### Typical use-cases:
- Freezing an older OS/demo/service
- Trying newer OS features
- Working out installation scripts for new installs
- Scaling hardware use across VMs
- Migrating VMs between servers as needed
- Disaster recovery - load a backup copy of a vital service





# References