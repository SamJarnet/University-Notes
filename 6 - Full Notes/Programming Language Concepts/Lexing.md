2026-04-08 14:07

Status:

Tags: [[Programming Language Concepts]]


# Lexing

#### Basic Concepts 
- Lexing analysis or lexing is the process of converting an input string into a sequence of tokens
- A lexeme is a pattern of characters in the input string that are considered meaningful in the given programming language.
	- These may be defined by regular expressions. 
- A token is a lexeme that has been identified and "tagged" with a meaning and possibly a value
	- "while" is a lexeme from the characters 'w', 'h', 'i', 'l', 'e' identified as the while-commands token
	- "true" is a boolean token with value true.

#### Scanning
- Lexemes are identified using a scanner that does the pattern matching
- Scanners most commonly use the "maximal munch" strategy
- Consume as much of the available input as possible to create a the lexeme
	- E.g. for pattern [1-9]+ and the input " ... 456, 234 ..."
		- There are lexemes "456" and "234" matching that pattern
	- For the pattern [1-9]+,[1-9]+ we would have "456,234" as a lexeme 

#### Maximal Munch Issues
- Can cause problems, depending on the language grammar.
- C++ has parameterised types known as templates:
		- e.g. template class vector $<t>$
- Parameters of templated classes can be templated classes: 
	- e.g. $vector< vector > //$ vector of vectors of integers 
- Parameters of templated classes can be expressions:
	- e.g. buffer $<$char, 256 $>$ buf;
![[Pasted image 20260408141634.png]]	
![[Pasted image 20260408141659.png]]

#### Evaluation 
- Tokens are created using an evaluator 
	- Analyse lexemes
	- Tag lexemes appropriately 
	- Identify any associated value 
- For example, given a pattern [1-9]+ and the input " ... 42 ...", as above:
	- We have the lexeme "42" 
	- The evaluator would tag this as an "integer" token whose value is the integer 42
- In Haskell, the function read is very useful for evaluation 

#### How to write a lexer
- Code must:
	![[Pasted image 20260408141955.png]]
- Code can be generic if:
	- We know what the lexemes look like
	- We know which lexemes correspond to which tokens 
	- We know how to associate values with tokens 
- If we have a means of describing these things, then we could just automatically generate the code to do the scanning and the evaluating

#### Lexer Generators
- Software tool, given an input that describes the lexemes and what tokens they produce, will generate code for you that performs lexical analysis.
- We use Alex for Haskell
# References