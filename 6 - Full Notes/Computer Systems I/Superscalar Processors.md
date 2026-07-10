22-12-2024 15:39

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Superscalar Processors

#### What is Superscalar?
- Common instructions (arithmetic, load/store, conditional branch) can be initiated and executed independently
- C = a + b
- D = e * f

#### Why superscalar? 
- Most operations are on scalar quantities
	- i.e. not vectors/arrays of data
- improve these operations to get an overall improvement

#### Limitations
- Instruction level parallelism 
- Compiler based optimisation 
- Hardware techniques
- Limited by 
	- True data dependency 
	- Procedural dependency 
	- Resource conflicts 
	- Output dependency 
	- Antidependency

#### True data dependency:
- ADD r1, r2  (means r1 = r1 + r2)
- MOVE r3, r1 (means r3 = r1)
- Can fetch and decode the second instruction in parallel
- Cannot execute second instruction until first is finished

#### Procedural Dependency:
- Can not execute instructions after a branch in parallel with instructions before a branch
- This prevents simultaneous fetches
- if (x+2) > y: 
	 y = y+1
	z = x + y

#### Resource Conflict:
- Two or more instructions requiring access to the same resource at the same time
	- two arithmetic instructions needing the ALU
- Can duplicate resources 
	- e.g. have two ALUs

#### Design issues:
- Instruction level parallelism (program property)
	- Instructions in a sequence are independent
	- Execution can be overlapped
	- Governed by data and procedural dependency 
- Machine Parallelism (hardware property)
	- Ability to take advantage of instruction level parallelism
	- Depends on how many exec units the CPU has


#### Instruction issue:
- Order in which instructions are fetched
- Order in which instructions change registers
- Order in which instructions change registers and memory 
- Try to look ahead for executable instructions
- Identify instruction parallelism and make use of it 


#### In-Order Issue, In-Order Completion: 
- Issue instructions in the order they occur
- Not very efficient (e.g. "spare" may ALU not used)
- May fetch > 1 instruction
- Instructions may stall if necessary
- useful baseline for comparison

#### In-Order, Issue Out-of-Order Completion
- Output dependency
	- R3 = R3 + R5; (I1) 
	- R4 = R3 + 1; (I2) 
	- R3 = R5 + 1; (I3) 
- I2 depends on result of I1 - data dependency 
- If I3 completes before I1, the result from I1 will be wrong - output (read-write) dependency

- Decouple decode pipeline from execution pipeline
- Can continue to fetch and decode until this pipeline is full
- When a functional unit becomes available an instruction can be executed
- Since instructions have been decoded, processor can look ahead


#### Antidependency
- Write-write dependency
	- R3 =R3 + R5 (I1) 
	- R4 =R3 + 1 (I2) 
	- R3 =R5 + 1 (I3)
	- R7 =R3 + R4 (I4) 
- I3 can not complete before I2 starts
- As I2 needs the value of R3 but I3 changes R3!

#### Register renaming:
- Output and antidependencies occur because register contents may not reflect the correct ordering from the program
- May result in a pipeline stall
- Dynamically allocating registers helps:
	- i.e. registers are not specifically named 
	- 50 - 100% speedup in some cases

#### Register Renaming example 
- R3b =R3a + R5a (I1) 
- R4b =R3b + 1 (I2) 
- R3c =R5a + 1 (I3) 
- R7b =R3c + R4b (I4) 
- Note R3a R3b R3c are versions of register 3  
- sorted out by the completion unit

#### Machine parallelism:
- Duplication of resources
- Out of order issue
- Renaming
- Need instruction window large enough (more than 8) to "see" the instructions coming in
- Out of order execution unit in Intel cores has a large buffer to manage this

#### Speculative Execution:
- If there is a unit free - could do instructions that may be needed (e.g. in if then else)
	- Out of order exec can provide this
- Provides another speed-up but:
- "Meltdown"

#### Superscalar Implementation:
- Simultaneously fetch multiple instructions
- Logic to determine true dependencies involving register values
- Mechanisms to initiate multiple instructions in parallel
- Resources for parallel execution of multiple instructions
- Mechanisms for committing process state in correct order

#### Summary 
- Superscalar design allows more than one instruction to be carried out simultaneously 
- It involves complex hardware optimization to work efficiently 
- Expect 2-4 instructions per clock cycle depending on core design and instruction mix
- Remember we’re talking about ONE core here

# References