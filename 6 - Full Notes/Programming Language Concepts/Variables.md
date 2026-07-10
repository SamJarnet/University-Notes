2026-02-04 13:49

Status:

Tags: [[Programming Language Concepts]]


# Variables

#### Definition 
- A placeholder for a value of some possibly complex type 
- e.g. in functional languages a variable can be higher-order (represent functions) 
	- this is a semantic concept - not just a memory location 

- Variables do refer to memory locations and some languages allow you to obtain location information (e.g. C pointers)
- The term aliasing refers to two variables pointing to the same memory location

#### Attributes
- 6 Attributes:
	- A name 
	- An address (aka an L-value left hand side of assignment)
	- A value (aka an R-value)
	- A type
	- An extent 
	- A scope 

#### Names
- Also called identifiers 
- Some case sensitive or length restrictive or lexical rules (e.g. only contain alphanumeric) languages 
- No canonical choice for naming schemes at the moment
#### Binding 
- A binding is an association between an entity and some attribute 
	- e.g. between a variable and its type
	- or between a variable and its scope 
- Static binding
	- Occurs before execution (compile time ) and remains unchanged throughout execution 
- Dynamic binding first occurs during execution (runtime) or changes during execution (runtime)

#### Allocation and Deallocation 
- We refer to the binding of a variable to its address as allocation 
- The complement is deallocation 
- Allocation can be static (initialisation time) or dynamic (runtime) 
- Deallocation is largely a dynamic concept 
- A variable's extent is the time between allocation and deallocation 

#### Four kinds of variables 
- Static Variables (aka. global variables) 
	- Bound to a memory location at initialisation time 
	- e.g. Static class variables in Java are static variables
- Stack-dynamic variables (aka. local variables) 
	- Memory is allocated from a runtime stack and bound when a declaration is executed and deallocated when the procedure block it is contained in returns.
	- e.g. Local variables in a method declaration

- Explicit heap-dynamic variables 
	- Nameless abstract memory locations that are allocated / deallocated by explicit runtime commands by the programmer 
	- e.g. malloc/free in C, new/delete in C++, all objects in Java using new()
- Implicit heap-dynamic variables
	- Memory in heap is allocated when values are assigned to variables. It is deallocated and reallocated with re-assignment. Error prone and inefficient. 
	- Used in ALGOL 68, LISP, C and JavaScript (for arrays)

#### Static Type Binding
- Two approaches to static type binding: 
- Type declaration
	- Most commonly used approach (used in C, Java, etc)
	- A variable is introduced with an explicit type and possible an initial value
- Type inference
	- No types in variable declarations; the type is inferred from the usage of the variable or by following a fixed naming scheme.
	- Primitive type interface - e.g. in Fortran I, J, K, L, M and N are Integer types, otherwise Real assumed. 
	- More sophisticated - Hindley-Milner inference introduced in ML has few annotations and the compiler deduces a most general type for a variable by its usage. The most general type is typically expressed using polymorphism or generics 

#### Dynamic Type Binding 
- Occurs as a variable is assigned to a value at runtime
- A variable's type binding can change during execution simply by assigning to it a value of a different type 
- Commonly used in scripting languages such as JavaScript, Lua, PHP, Python.
- Efficiency implications (both time and space) due to runtime type checking 
- Arguably advantages in readability and coding convenience

#### Extent
- The extent (or lifetime ) of a variable refers to the periods of execution time for which it is bound to a particular location storing a meaningful value 
- Extent is a semantic concept and depends on the execution model
- A running program may enter and leave a given extent many times, as in the case of a closure.

- Different kinds of variables have different extents.
	- Static variables have an extent of whole program execution 
	- Stack-dynamic variables have an extent of a particular stack frame or procedure call
	- Explicit heap-dynamic variables have an extent from explicit allocation to explicit deallocation (cf. garbage collection and memory leaks)
	- Implicit heap-dynamic variables have an extent from implicit allocation to implicit deallocation (values may persist in memory but addresses are freed)


#### Scope 
- Local variables are declared within a program block; the block is the scope of the variable 
- Static variables have whole program scope, except where they are temporarily hidden by a locally scoped variable with the same name
- We refer to lexical scope where scope is aligned to statically determined areas of source code e.g. a class definition, a code block, or method body.
	- A lexical concept, not a semantic concept 

#### Dynamic Scope 
- Determined at runtime only as it depends on control flow
- Imagine a stack of value bindings for each variable that is updated with the control stack 
- A variable is in a dynamic scope if its name is meaningful within the bindings of the current call stack

- Uncommon in modern programming languages as it flies in the face of referential transparency
- Example: 
	![[Pasted image 20260406210906.png]]
	- y is lexically scoped and is local to "first" 
	- x is dynamically scoped and is still in scope when calling "second()"
	- If "second()" were called not via "first()" then x would not be in scope 


# References