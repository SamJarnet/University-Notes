03-10-2024 16:30

Status:

Tags: [[Data Management]] [[Computer Systems I]] [[Operating Systems]] 


# Linux

#### Definition: 
Free and [[Open source]] OS which is based on the [[UNIX]] OS. 

#### Security of Linux:
- Largely "Virus-free"
	- Almost no viruses written for Linux
	- Normal user accounts have limited access to rest of the system making corruption of system binaries much harder
- Modular system architecture
	- Clear separation of the kernel from the rest of the OS components. 
	- This makes it hard for bugs in GUI applications to crash the entire system

#### Versus windows:
Linux is much cheaper

#### A few essential commands:
- ls: list files
	- -l long list (displays lots of info) 
	- -t sort by modification time 
	- -S sort by size 
	- -h list file sizes in human readable format (bytes instead of blocks) 
	- -r reverse the order
	- options can be combined too e.g. ls -ltrh
- cat myfile: prints file to screen
- sudo command: runs command as supervisor
- pwd: shows your path
- cd location: takes you to specified location (none takes you to home location)
- chmod: used to change/add permissions to a file
- [[File Handling]]


#### File permissions:
- In Linux, files have three sets of permissions
- User, Group and Others.

Disks, USB ports etc. are represented as files. There are also helpful files that do a simple job like:
- /dev/zero
- /dev/null
- /dev/urandom
- /etc stores config files for the system
- /var/log stores log files for various system programs
- /bin and /usr/bin stores several commonly used programs
- ~ (tilde): Shortcut to your home directory. 
- E.g. : /home/students/downloads is the same as ~/downloads
- . (dot): A reference to your current directory.
- .. (dot dot): A reference to the parent directory. You can use this several times in a path to keep going up the hierarchy.

#### Paths:
All files and directories can be referred to using both types of paths:
- Absolute paths: Specify location in relation to the root directory.
	- Indentification hint: they always begin with a forward slash (**/**)
- Relative paths: Specify a location relative to where we currently are in the file-system. They don't begin with a forward slash
#### Try things on your ECS Linux server:
- Log into server using Putty with username: linuxproj.ecs.soton.ac.uk
- Or open CMD and type: ssh scj1g24@linuxproj.ecs.soton.ac.uk



# References