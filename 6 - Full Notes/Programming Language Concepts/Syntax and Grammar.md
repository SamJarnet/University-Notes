2026-04-06 21:12

Status:

Tags: [[Programming Language Concepts]]


# Syntax and Grammar

#### Syntax vs Semantics 
- Syntax 
	- This refers to the structure of statements in a program
	- It typically follows a grammar based upon certain lexical symbols (e.g. keywords in a language)
- Semantics
	- This refers to the meaning of programs and how programs execute 
- The role of an interpreter or compiler of a language is to transform syntax into semantics 

#### Language Syntax as Grammars 
- Most languages can be represented by a CFG
- BNF form is the standard for defining the grammar for a language

#### Non-Terminals vs Terminals 
- BNF acts as a meta-language for defining languages 
	- It is a convenient meta-syntax for defining the grammar of a language 
- Non-terminals represent different states of determining whether a string is accepted by the grammar.
	- In programming language terms, these refers to the kinds of expressions one may have in the language.
	- e.g. class level declarations, method declarations, statements or expressions.
- Terminals represent the actual symbols that appear in the strings accepted by the grammar 
	- These are sometimes called tokens or lexemes and refer to the reserved words, variable names and literals of our programs.
- e.g. 
	![[Pasted image 20260406212227.png]]
- Non terminals written as <"follows">  AND terminals written in bold

#### Parse Trees
- The legal programs of a language are those strings for which there is a derivation in the BNF grammar for the language 
- A derivation of a string in a BNF can be represented as a tree
- At each node, the tree represents which rule of the grammar has been used to continue deriving the string 
	- The child nodes represent the matches of the substrings according to the grammar 
- e.g. for 2 + 3 * 4*
	![[Pasted image 20260406212618.png]]


#### Syntax to Execution 
- We can understand programs as a string of text, parsed as a tree according to some grammar, usually expressed in BNF 
- How do we find the derivation of a string in a grammar? 
- Step 1- Lexing 
	- Involves in translation the particular symbols or characters in the string that make up the terminals of the grammar into tokens 
- Step 2 - Parsing
	- Involves translating the sequence of tokens that make up the input string into a tree. The parser must follow the rules of the grammar and build a tree representing the derivation.
- In this latter step we often move away from parse trees and work with ASTs.

#### Abstract Syntax Trees
- Grammar:
	![[Pasted image 20260406212903.png]]
-  E.g. while (x < 4) do { print (x++) * 4 ; } 
	![[Pasted image 20260406212945.png]]
- Simplified:
	 ![[Pasted image 20260406213017.png]]
- This tree retains the structure of the code, but abstracts away the syntax that's used only to shape the tree.
- These are ASTs 
- These are the structures that compilers and interpreters work with


#### Ambiguous Grammars 
- We say that a grammar G is ambiguous if there exists a string s for which there exist two or more different parse trees for s using the rules of G 
- Ambiguity in programming language grammars is generally considered a bad thing 
- Two different parse trees for the same string of symbols implies two potentially different semantics for the same "program" 
 	- e.g. what does "2 + 3 * 4" evaluate to with an ambiguous grammar.

#### Resolving Ambiguous Grammars 
- We could put parentheses everywhere 
	- This is effective but impacts readability.
- We could use operator precedence:
	- We can ask that one operator "binds tighter" than another operator; we say that the operator would have higher precedence 
	- e.g. * binds more tightly than + so * has a higher precedence than +
	- We understand "2 + 3 * 4" implicitly as "2 + (3 * 4)"
	- n.b. higher precedence operators will appear lower in the parse tree

#### Changing associativity
- Does associativity matter?
	![[Pasted image 20260408140306.png]]
	- 2 + (3 + 4) means the same as (2+3) + 4 anyway
	- But 2-(3-4) is not the same as (2-3) - 4
- How would we guarantee left associativity?
	![[Pasted image 20260408140331.png]]
	- Be careful doing this as left recursive grammars don't work well  with recursive descent 

#### The Dangling Else Problem
- In many programs you can write an "if-then" statement without the "else" branch
- Consider the grammar:
	![[Pasted image 20260408140450.png]]
- Does the following terminate:
	![[Pasted image 20260408140538.png]]
	- No it loops forever.
- The grammar for Java contains a solution
- Addition non-terminals are used to determine a precedence that a nested conditional in a "then" branch cannot use a single branch conditional
	![[Pasted image 20260408140705.png]]



# References