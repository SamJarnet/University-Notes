22-10-2024 12:07

Status:

Tags: [[Data Management]] [[Linux]] 


# Structured Data

#### Structured Data:
- We can easily manipulate it and process it
- CSV, TSV are two popular formats of structured data for representing rows and columns
	- Comma Separated (CSV)
	- Tab Separated (TSV)
- [[UNIX]] tools such as cut, sort, grep, paste, join, etc are all designed to work with them

#### We have to be careful:
- New lines are a right pain… 
	- /r = Carriage Return (Back to the start) 
	- /n = New Line (Feed up a line)
	- Windows uses /r/n, Mac and Linux now use /n 
	- Some things still use just /r


#### Sometimes we need more:
- CSV/TSV isn't enough
- Fixed column and row format
- Have to be talking about the same thing in the same way
- Works well for some cases (particularly lists)
	- E.g. Lists of students, news articles, locations etc.
- Doesn't work well in other cases (flexible formats)
	- E.g. Document representation, conversations, annotations etc.
	- Relational data
	- Multiple different types - one file, but describes modules, students, exam marks, etc.

#### YAML:
- Originally “Yet Another Markup Language”… 
- ..but now “YAML Ain’t Markup Language” 
- Widely used in config files 
- Technically a superset of JSON
- Relies on whitespace for structure, rather than tags 
- Easier to read! (Yay?) 
- Harder to write! (Boo!) 
- Key-value pairs
Example:
![[Pasted image 20241029111744.png|300]]

#### When/why would I use it? Why wouldn’t I use it? 
- Config files 
- Passing messages between applications 
- Saving (simple) application state 
- Spec is someone ambiguous – not all parsers will give the same result! 
- Not as widely used as some other data serialisation formats

#### JSON 
- JavaScript Object Notation 
- 3 important concepts 
	- Objects
	- Lists 
	- Values 
- Objects, but no classes!

#### Benefits of being understandable by machine?
- Searching
- Aggregation and Summarisation
- Prediction
- Linking

#### Human vs. Machine:
- Human-readable
	- Text, images, forms
	- Mostly unstructured
	- Focus on usability
- Machine-readable
	- Needs to be structured
	- Machines can't yet "read"
	- Focus on efficiency
	- Generally not human readable/writeable
#### Both-readable? [[Markup]]! 
- Annotating a document to add metadata 
	- Presentation
	- Structure
	- Describing content
	- Adding meaning
	- Aiding processing by tools
- Like the “marking up” of manuscripts
# References