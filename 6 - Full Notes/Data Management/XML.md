29-10-2024 11:41

Status:

Tags: [[Data Management]] [[Structured Data]] [[Markup]]


# XML

#### XML: eXtensible Markup Language
- Hierarchical
	- Tags
	- Attributes
	- Content
- Designed to carry data, not display data
- No defined tags
	- You define your own XML tags
- Meta-tools to define purpose of specific tags
	- DTD: Document Type Definition
	- Schema
- Unicode
- W3C recommendation (1998)

#### XML Syntax:
- All XML elements must have a closing tag
- XML tags are case sensitive
- XML elements must be properly nested
- XML Documents must have a root element 
- XML attributes must be quoted e.g. $<tag$ attr="...">

#### Elements or Attributes?
- We can use 
- ![[Pasted image 20241105130259.png]]
- Which should we use?
	- There is no strict definition!
	- Generally, use an attribute if it's "meta-data" rather than data
	- Use an element if it is in a relationship with its parent and and could exist outside the tag - or if it's something that you might need to know the metadata of!

#### Namespaces: The problem:
- Back to XML
- XML files can reference and include 

# References