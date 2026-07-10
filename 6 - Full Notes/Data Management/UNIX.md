03-10-2024 17:12

Status: 

Tags: [[Data Management]] 


# UNIX

#### Definition:
- A small [[Operating Systems]] for time-shared computing.
#### Philosophy of UNIX:
Set of cultural norms and philosophical approaches for minimalistic software development.

- Make each program do one thing well. To do a new job, build afresh rather than adding to old programs.
- Expect the output of every program to be the input to another, so don't clutter your outputs.
- Design and build software even OS, to be tried early, ideally within weeks. Throw away bad parts and rebuild them.
- Use tools rather than unskilled help to lighten a programing task. Even if you have to detour to build the tools and throw them out.

Code is short and simple to reduce the effort taken to debug.

#### Meta-information on UNIX files:
- Meta-information on a UNIX file is stored as an Index Node
	- Inode data structure
- A Inode data-structure is referenced by a number
- A UNIX directory contains a table of the names of files it contains and their respective Inode numbers
- Keeping separate from the contents of the file allows files to move from one directory easily and fast. A user can rename or delete a file even if has opened it and is working on it, so no application can "hijack" a file

# References

[[Pipes and Filters]]