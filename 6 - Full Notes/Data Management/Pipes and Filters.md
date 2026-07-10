08-10-2024 12:03

Status:

Tags: [[Data Management]] [[UNIX]]


# Pipes and Filters

#### Input/Output Redirection ("piping"):
- Bash shell allocates three file descriptors for each process
	- STDIN is opened for keyboard input
	- STDOUT, STDERR to screen output
- We can change these.
- Programs (or filters) can output to other programs which is called "piping"
- The output of one program becomes the input of another
- >> is used to append to the end of a text file instead of > which overwrites
- < is used to take the file as input

#### Filters: 
- A filter is a program which accepts textual input and transforms it in some way
- Filters can be connected using pipes
- Used as "building blocks" to be easily put together to do what you want


Examples:
- head: view the first 10 lines of data
- tail: last ten lines of data
- sort: sort in order
- wc: print a count of lines, words and characters
- uniq: remove duplicate lines
- du: estimates file space usage
- xargs: builds and executes command lines from standard inputs
- cut f k: where k is a column. Displays whole column 

#### Examples of piping with pipe operator | :
- The pipe operator (|) creates concurrently executing processor for each filter used.

#### Useful commands:
- find: search for files in directory hierarchy
- tar: create a file archive / extract from a file archive
- gzip/gunzip & zip/unzip: used to compress/decompress files
- nohup: a way to run a command in the background
- parallel: a tool used to run jobs in parallel
- basename: strip directory from filename
# References