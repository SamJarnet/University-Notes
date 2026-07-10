2026-04-08 15:49

Status:

Tags: [[Programming Language Concepts]]


# Type Systems

#### Definition
- A tractable syntactic method for proving the absence of certain program behaviours by classifying (program) phrases according to the kinds of values they compute

#### What are types?
- Types are abstract descriptions of programs. We can study the correctness properties of interest by abstracting away all of the low-level details. 
- Types are precise descriptions of program behaviours. We can use mathematical tools to formalise and check these interesting properties. 

#### What do types do for us?
- Guarantee absence of certain behaviours
	- Doesn't let you add two different types together or access a third dimension of a 2D array.
- Enforce higher-level modularity properties.
	- Encapsulation 
- Types enforce disciplined programming.
	- Type systems form the backbone of module based languages for large-scale composition 
	- Types are the interfaces between the modules
	- Types encourage abstract design 
	- Types are a form of documentation 

#### Approaches to Using Types
- Strongly Typed: Check use of data to prevent program errors
- Weakly Typed: Errors may happen; types are used for other purposes such as memory layouting
- Static Typing: Type checking occurs at compile time 
- Dynamic Typing: Type checking that is delayed until run time 

#### Strong vs Weak Typing 
- Strong typing requires that whenever an object is passed from a calling function to called function, its type must be compatible with the type declared in the called function 
- This definition generalises to the same requirement on any consumer of data 
- Let's consider a language to have weak typing otherwise 
- Strong Typing implies that types must be declared/inferred with functions/methods. This can make languages verbose, e.g. Java.
- Weak Typing implies that data of the "wrong" type may be passed to a function - and the function is free to choose how to behave in that case. Typical solution - implicit data coercion, which can go wrong.

#### Static vs Dynamic Typing 
- Statically typed languages often use an approximation of the run time type of values.
	- E.g. if True then 1 else 2 + "hello"
- Why? Because statically determining control flow is undecidable (in sufficiently rich languages)
- Compile time checking can avoid costly runtime errors 
- Where types are used for memory layout, static typing is appropriate (e.g. C)

- Dynamically typed languages check the types of data at point of use in run time.
	- Exact types; no false negative type errors 
	- Often allow variables to change their type, or objects to dynamically grow new methods
	- Common in scripting languages and web programming.
	- Should not be used for Critical Systems as errors may be detected too late.


## Type Checking and Type Safety

#### When do we check Types?
- For statically typed languages we check types during compilation.
	- In the compilers front end - type checking is done on program's abstract syntax tree and is sometimes referred to as semantic analysis.
	- Some strongly typed languages insist that variables are manifestly typed; some use type inference, allowing the compiler to work out suitable types automatically.
- This means that there exists a part of the compuiler that guarantees some correctness for the programs that pass type checking.
	- This is some sort of algorithm coded up in a high-level language, or even C.
- How do we know we can trust this type checking algorithm? Do we really know that it gives us what is called type safety

#### Type Safety 
- Show it doesn't go wrong

# References