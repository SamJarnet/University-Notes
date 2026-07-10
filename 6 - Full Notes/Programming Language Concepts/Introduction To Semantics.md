2026-04-15 14:19

Status:

Tags: 


# Introduction To Semantics

#### What does it take to prove Type Safety?
- Inductively defined typing relation - a bit like a proof in propositional logic
- Inductively defined reduction relation - i.e. how the program runs
- Description of error states in the program
- We use the mathematical descriptions to try prove that type safety holds for a given language

#### Semantics
- Refers to the meaning of programs 
	- a semantics of a program is a specification of a programs runtime behaviour. What values it computes, what side effects it has etc.
	- The semantics of a programming language is a specification of how each language construct affects the behaviour of programs written in that language
- The most definitive semantics of a program is its compiler or interpreter.
	- If you want to know how a program behaves, run it.

#### Why we need formal semantics
- Compilers and interpreters are not so easy to use for reasoning about behaviour. Why?
	- Not all compilers agree
	- Compilers are large programs, it is possible and common that they contain bugs themselves. So the meaning of programs is susceptible to a compiler writer error
	- The produced low-level code is often inscrutable. It is hard to use compiler source code to trace the source of subtle bugs in your code to strange interpretations of language operators.
	- compilers optimise programs (allegedly in semantically safe ways) for maximum efficiency. This can disturb the structure of your code and make reasoning about it much harder.

#### Advantages of formal semantics
- In contrast, a formal semantics should be precise (like a compiler) but written in a formalism more amenable to analysis. 
	- This could be some form of logic or some other mathematical language
	- Don't need to worry about efficiency of execution and can focus on unambiguous specification of the meaning of the language constructs. 
	- Can act as reference "implementations" for a language: any valid compiler must produce results that match the semantics. 
	- They can be built in compositional ways that reflect high-level program structure. 

#### Approaches to Semantics 
- There are three common approaches to giving semantics for programs: 
	- Denotational Semantics advocates mapping every program to some point in a mathematical structure (domain) that represents the values that the program calculates.
		- e.g. $[[$ if (0<1) then 0 else 1 $] ]$ = 0
	- Operational Semantics uses relational approaches to specify the behaviour of programs directly. Typically inductively defined relations between programs and values they produce, or states the programs can transition between are used.
		- e.g. if (0<1) then 0 else 1 → if (true) then 0 else 1 → 0
	- Axiomatic Semantics take the approach that the meaning of a program is just what properties you can prove of it using a formal logic.
		- E.g. Hoare Logic 

#### Denotational Semantics 
- To give a denotational semantics one must first identify the semantic domain in to which we will map programs
- Elements in the semantic domain represent the meanings of programs
	- E.g. for programs that return a positive integer, a reasonable choice of semantic domain is the natural numbers.
	- For programs that represent functions from integers to integers we would choose the set of all functions between naturals
	- For programs that return pairs of integers we take the semantic domain to be the Cartesian product of the set of natural numbers with itself, etc.
- Semantic domains are built by following the structure of the types of the language.
- In an ideal language, the structures on the types of would make for well-known, simple mathematical structures in the semantic domain.
- This is not always the case, side-effects, loops and recursion complicate things.

#### Denotational Semantics for the Toy Language
- Grammar:
	![[Pasted image 20260415144500.png]]
- First, we choose the semantic domains. These will be $N$ and a different two element set B = {true, false}. We will also make use of the function spaces between these sets. Let's define $[[T]]$ to be $N$ when T is Bool and define $[[T \rightarrow U]] = [[T]] \rightarrow [[U]]$.
- Our aim now is to provide a function $[[-]]$ from well-typed programs E of type T to the semantic domain $[[T]]$, that is:
	- Given $⊢ E : T$, then $[[E]]$ should be a value in $[[T]]$.

#### Interpreting Type Environments
- Of course, in trying to interpret functions we will need to interpret function bodies.
	- These may contain free variables 
	- We will need to interpret terms with possible free variables in them.
- We need to have an environment to provide values for the variables.
- Given a term $\Gamma ⊢ E : T$ then we need an interpretation of $[[E]]$ that makes use of an environment $\sigma$ that maps each free variable in $\Gamma$ to a value in the semantic domain. We write $[[E]]_\sigma$ to denote this.
	- We say that $\sigma$ satisfies $\Gamma$, written as $σ ⊨ \Gamma$, if whenever $\Gamma(x) = T$ then $\sigma(x)$ is a value $[[T]]$
	- We require the property that, for $\Gamma ⊢ E : T$ and for all $\sigma$ such that $σ ⊨ \Gamma$, then $[[E]]_\sigma: [[T]]$ 

#### Defining the Denotation Function for Toy
- Let's start with the value and variables of the language and arithmetic expressions.
	![[Pasted image 20260415151131.png]]

#### Comments on Denotational Semantics
- A criticism one might have of denotational semantics at this point is that they don't give a very clear account of how the program is actually supposed to execute. 
- Instead, they give a very precise and nicely compositional account of what values the program is supposed to calculate. This abstracts away all of the execution steps. 
- This can be useful for modelling pure functional languages, but it can be trickier for modelling languages with mutable state or concurrency.
- Modelling recursion denotationally can also be challenging - what value does a non-terminating recursive loop get mapped to?
- A criticism of the denotational model of Toy is that there is a lot of junk
- $[[Int \rightarrow Int]]$ is all functions from N to N - this will include un-computable functions. The model is "too big". 







# References