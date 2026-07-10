.11-10-2024 09:16

Status:

Tags: [[Data Management]] [[Linux]] [[UNIX]]


# File Handling

#### grep
grep is a command to search input given to it. 
- It looks for lines in the input that match a particular pattern or regular expression
- Usage: grep pattern input
- The pattern can be constructed from regular expressions.

#### sed
sed is a text stream editor
- Reads input and modifies it as specified by a list of commands. The modified input is then written to the standard output. 
- Usage: sed [options] command [file ...] 
- Most commonly used command is to substitute text with something else
E.g. echo Hello World | sed "s/Hello/Hi/I" produces output: "Hi World"
The I flag allows you to substitute in a case insensitive manner

E.g. cat smallfile.csv | sed 's/,/\t/g'. Replaces all commas in a csv with slashes.
The g flag allows you to substitute globally, not just the first instance of the match on each line.

#### awk
awk is a utility for processing structured text files: rows & columns:
- Regards each line in a file as a record 
- Each line broken into fields
- ‘The quick brown fox’: ‘The’, ‘quick’, ‘brown’ 
- Good to parse tables (tab-delimited)

# References