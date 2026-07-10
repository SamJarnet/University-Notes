2026-01-01 19:50

Status:

Tags: [[Artificial Intelligence]]


# Meaning and Value

#### Science and Objectivity and Reductionism 
- Central idea:
	- Modern science has achieved great success by stripping away the "subjective" to find "objective truth". However, this process (reductionism) removes the very context where "meaning" and "Value" exist
- Philosophy: "Study of fundamental nature of knowledge, reality, and existence" == the nature of everything 
- Science is a subset of philosophy - an approach developed since 3000 BC refined by philosophy 
- The scientific revolution -> scientific method:
	- Observation/idea -> testable hypothesis 
	- Testing: Experiment -> evidence 
	- Conclusion: is evidence consistent with hypothesis? -> eliminate untruths/refine hypothesis 
- Science should be reason free from passion: no agenda, no aim, only "truth"
- The agenda of science is to remove the subjective and the personal
	- It values objectivity > subjectivity
	- It calls objectivity = "truth" (because it is independent of the observer)
- Reductionism:
	- Searching for understanding by taking things apart and looking at its parts and how they interact
	- The issue:
		- It is argued reductionism dismantles meaning. If a human is just a collection of atoms, or a brain is just a series of firing neurons, the "meaning" of a person's life is lost in the mechanical description.
- The value problem:
	- Science can tell us how things work, but it cannot tell us why they matter
	- This leads to a "loss of meaning" in a socio-cultural context, contributing to global crisis (e.g. the tragedy of the commons) where we treat the world as a meaningless machine to be exploited 

#### Brain Science and Cognitive Styles (The master and his emissary)
- Central idea:
	- Argues that the human brain has two distinct ways of "processing" the world. The AI we build today is almost entirely a model of the Left Hemisphere 
- Left Hemisphere (LH) Style:
	- Traits: Logical, decontextualised, formal, mechanical, and focused on parts
	- Relationship to AI: Modern AI (algorithms, logic, data processing) is an extension of the LH. It "Thinks" it doesn't need context or the "subjective" to be complete 
- Right Hemisphere (RH) Style:
	- Traits: Analogical, contextual, informal, holistic and focused on relationships
	- Meaning and Value: The lecture asserts that meaning and value reside in the RH because they require context and connection, which the LH (and current AI) cannot grasp
- The power dynamic: The LH acts as an "emissary" that has forgotten it serves as a "master" (the RH). In AI terms, we are building hyper-efficient "Emissary" (AGI/LLMs) without the "Master" (Contextualised meaning)

#### Formal Systems and the Incompleteness of AI
- Central Idea: It is argued that the limitations of AI are not just biological but mathematical and fundamental
- Incompleteness:
	- Godel: Any formal system has inherent limitations
		- There are true statements that cannot be proved within the system
		- "This statement is not provable in this system" 
		- If the system is consistent, this statement must be unprovable and true, revealing that truth and provability are not identical.
	- Computability:
		- Undecidability. Halting Problem. "This program continues if it halts"
	- Diagonal argument (Cantor): assume you can enumerate the set of true statements, then construct a diagonal statement that isn't in that set
	- Limitations of proof (within any formal system
	- To formalise a system we must cut it off from context - so that its rules are not context sensitive (OBJECTIVE). Godel sentences create a self referential context (SUBJECTIVE)
- Learning with generalisation 
	- Requires we go beyond the data, beyond what is logically supported
	- We aren't memorising data
	- We are only interested in performance on the test set not the training set
- Learning is an inductive inference process 
	- Deductive: 
		- All men are mortal
		- Socrates is a man
		- Socrates is mortal
	- Inductive
		- The swan is white
		- The swan is white
		- All swans are white
	- Deduction is logically sound and induction is not 
	- Induction is essential for generalisation:
		- e.g.to learn general concepts/class from specific examples/instances
- Generalisation:
	- Being able to give an appropriate response for a situation where you have not been already told the appropriate response
	- == going beyond the training data
	- depends on inductive bias
- Inductive bias: 
	- From the set of all models that are consistent with the data, some models are preferred over others. That is the inductive bias.
		- Common inductive bias is simplicity: Occam's razor. Parsimony pressure.
		- e.g. "all swans are white" > "all swans are white or pink", "the first 10 swans are white"
	- It cannot be eradicated: The set of models that are consistent with the data is unbiased iff all possible predictions are equally represented. == not making any prediction in particular == NOT generalising (just telling you exactly what is in the data and nothing more)

- Substrate independence 
	- "algorithms" are substrate independent = "multiply realisable" 
		- e.g. with electronics, or analogue hardware based NN, or hydraulics or valves, beer cans and strings 
	- If the computational substrate "shows through" to the behaviour, then it is not substrate independent (by definition)
	- e.g. If any of these, then substrate shows through = not algorithmic 
		- If my computer gets hot and starts doing logic differently,
		- If small differences between one part of the RAM and another means that each time I load the program I get different results 
		- If the order or timing of how i Load the program matters to results 
	- Computational functionalism:
		- Mental states are definedf by their computational roles (what they do rather than the physical material they are made of).
		- The mind is like the software ( the brain / hardware doesn't matter )

- The substrate shows through on neural networks for example XOR and NAND cant be represented linearly so you use two nodes and now the representation of XOR and NAND change based off the start conditions. This means that the way that the network generalises is not defined by the data 
- Comes down to tiny differences in initial conditions
	- Tiny differences between the initial values of weights and thresholds 
	- Differences in timing/order of training sample presentation 
- The way that a network generalises is the way that its underlying (non-rational) nature "shows through" to its behaviour 
- In this  sense, the way a network generalises is not substrate independent, not algorithmic
- the only thing that the learning system contributes beyond the training data is the way that it generalises  = its inductive bias = what was NOT formally given by the training data/past 

#### How does your substrate show through?
- Informal is required
	- Even in this minimal example, we can see that formal systems have their limits. And the way the behaviour goes OUTSIDE the formal limits is exactly the thing/the only thing that is interesting about it. 
		- Depends on "irritating details" - its non formal nature
	- Computational functionalism (the idea that we are substrate independent software with the right function) depends on details NOT mattering. But they do.
- Your non-formal nature, the way your substrate shows through, is not a failing - everything that is valuable about you depends on it 
- To be formal, the rules of a system must be decontextualised so that they are not context sensitive, they are true forever and always and from all points of view, not just in particular circumstances == objective, independent of observer/not subjective
- Formal = free from subjective context/decontextualised (in a bubble) 
- When we do inductive learning, we are bringing something to the process that is outside that bubble
- Is the inductive bias "truly valuable" or "stochastic/random/nonsense"?
- It is valuable if it generalises well, and not otherwise. What matters is the test set and the relationship to the larger more general context

-  How to get induction right
	- Option 1 - look at the answer - the test data
		- scrape internet train on everything
		- Prove you are right (in that larger but limited context)
	- 2 - prepare : build a learner with suitable in built bias
		- use the larger context to create common ground. a learner built from the same stuff, ready to learn things easily from that teacher, then just do the learning with that tuned in learner 
	- 3 - trust (that the preparation has already been done)
		- Trust that you and the context out there are already built from the same ground truth
		- Then you do you. Let your informal nature show through, thats where prior knowledge of the ground truth resides
	

- Your substrate shows through when stressed but most of the time its fine

 - How can one system really understand another?
	 - In order for me to learn about you
	 - I can make observations, and talk to you
	 - You cannot really communicate who you are inside through this interface
	 - If you tell me everything about you that matters, then I could just memorise it. But what you want me to do is infer (induce) a model of you from these samples
	 - Iff my inductive bias is appropriate, I can do this generalisation well
	 - An appropriate inductive bias cannot be inferred from the contact we have, it comes from something we already share: shared cultural and educational context, shared evolutionary history, shared biological substrate
	 - Learning requires that the learner and the learnee are already similar
- How can i know if another person is generalising appropriately about what is good for me? 
	- Deep down they are like me. They are human and hjave personal experience that resonates with mine
		- Friendship is based on love not facts
		- deeply vulnerable mutual knowing
	- If they are not like me deep down - it is ill advised to allow myself to be vulnerable to them 
- When does your substrate show through?
	- we can feel it in our heart when something we know is right but goes against rules
	- 
# References