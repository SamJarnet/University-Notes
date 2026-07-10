29-10-2024 11:33

Status:

Tags: [[Data Management]] [[Structured Data]]


# Markup

#### Metadata:
- In addition to real-world data, we often need to add more data
- Data that is useful for the machine but not for the human
- This metadata is typically stored alongside the main content
	- Often as annotations

#### SGML: Standard Generalised Markup Language 
- An ISO standard for defining Markup Languages (1986)
- Marking up the content
- A Super set of all markup languages
- Separates structure from content
- Metalanguage: Describing formatting and markup languages

- Tags: $<tag> ... </tag>$  
- Attributes: <tag attribute $=$"value">
- Content $<tag>$Content Goes Here$</tag>$

- Common subsets of SGML 
	- [[XML]] (including XHTML) 
	- [[HTML]]
	- OED (The Oxford English Dictionary)
- These are all SGML, but not all SGML are XML/HTML

#### From SGML to XML:
- SGML very flexible
	- You can do a lot! 
	- But very complex…
	- No strict structure
	- A lot of things had to be inferred
	- Requires a definition of the structure as well as the SGML itself

- XML was designed to be less flexible
	- Easier and more efficient to parse 
	- Simplifies SGML, while keeping the bits that were needed 
	- Data can be delivered without a definition of structure


# References