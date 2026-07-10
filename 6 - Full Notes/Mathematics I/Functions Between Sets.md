09-10-2024 16:44

Status:

Tags: [[Mathematics I]], [[Sets]], [[Operations on sets]], [[Relating sets]]


# Functions Between Sets

#### Notation:
A function f from set X to set Y is usually written:
- f : X -> Y
- X is called the domain
- Y is called the codomain
- We write f(x) = y to mean that the value of f at x is y 

#### Domain range:
Domain:
 - For each element x of the domain, there is exactly one element y of the codomain: the value of f at x.
 Range (or image):
 - The largest subset R ⊆ Y of a function f : X -> Y that satisfies:
	 - for all r ∈ R there exists x ∈ X such that f(x) = r
- In other words, the range is those elements of Y that are "mapped to" by f

#### Creating Functions:
The total number of functions you can construct from a set of size X to a set of size Y is $|Y|^{|X|}$ .
|Y| x |Y| x |Y| … |X| amount of times.

Is there a set X with exactly one function to it to any other set Y (X -> Y)
- Yes, $|Y|^{|\emptyset|}$ = $|Y|^0$ = 1 function X = $\emptyset$ 

Is there a set X with exactly one function from it to any other set Y (Y -> X)
- Yes, $|Y|^{|X|}$  -> |X| has to be 1, so any set X where it has one element (X={a})

#### Functions of several variables:
A function of several variables is nothing but a function where the domain is a cartesian product of sets (Multiple inputs). 

Examples:
- Addition, multiplication, etc can be considered functions
- e.g. $+: \mathbb{N} \times \mathbb{N} \rightarrow \mathbb{N}$  defined $+((k, l)) = k + l$ 
	- instead of $+((k, l)$ we often right $(k, l)$

- Let $\mathbb{2} = (0, 1)$ Binary logic gates can therefore be thought of as functions: 
  $\mathbb{2} \times \mathbb{2} \rightarrow \mathbb{2}$ 
  
 Example: 
![[Pasted image 20241028214333.png]]

S(x) = x-1 does not define $\mathbb{N} \rightarrow \mathbb{N}$ as if x=0 S(x)=-1 which is not in $\mathbb{N}$

Which one of the following are functions $\mathbb{R} \rightarrow \mathbb{R} ?$  
$f(x) = x^2$ Yes
$f(x) = 0$ Yes
$f(x, y) = x + y$   No as this is $\mathbb{R} \times \mathbb{R} \rightarrow \mathbb{R}$ 
$f(x) = \pm \sqrt{x}$ No as it has to map one-to-one
$f(x) = \text{number of primes } p \text{ where } 0 < p < |x|$ Yes

#### Composition:
If f : X→Y and g : Y→Z then f ; g : X→Z is a function that is defined 
- (f ; g)(x) = g(f(x)) 
- f ; g is sometimes written g∘f

#### Associativity:
Function composition is associative: (f ; g) ; h = f ; (g ; h)
- It is also true that $id_X ; f = f = f ; id_Y$

#### Inverting Functions:
Given a function f : X→Y, an inverse (if it exists) is a function f-1 : Y→X such that
- f -1(f(x))=x and • f (f -1(y))=y 
- This is the same as saying that $f ; f^{-1} = id_{X}$  and  $f^{-1} ; f = id_Y$

[[Taxonomy of Functions]]