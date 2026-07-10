22-12-2024 22:18

Status:

Tags: [[Computer Systems I]] [[CPU]]


# Pipelines

#### Pipelining:
- Fetch instruction
- Decode instruction
- Calculate operands
- Fetch operands
- Execute instruction
- Write/complete result
- Pipelines overlap these operations and aim to complete an instruction every clock cycle


#### Branch can cause a Pipeline “stall”
- Classic RISC pipeline: 
	- No calc or fetch operands (CO,FO)

#### Dealing with Branches:
- Multiple Streams
- Prefetch Branch Target
- Loop buffer
- Branch prediction
- Delayed branching

#### Multiple Streams:
- Have two pipelines
- Prefetch each into a seperate pipeline
- Use appropriate pipeline
- Leads to bus and register contention
- Multiple branches lead to further pipelines being needed
  
  
#### Prefetch Branch Target:
- Target of branch is prefetched in addition to instruction following branch 
- Keep target until branch is executed 
- Used as far back as IBM 360/91


#### Loop Buffer:
- Very fast memory stores last N instructions in sequence
- Maintained by fetch stage of pipeline
- Check buffer before fetching from memory
- Very good for small loops or jumps
- c.f. cache
- Used by Intel CPUs

#### Branch prediction (static):
- Predict: never taken
- Assume that a jump will not happen
	- Always fetch new instruction
	- Used in old designs 
- Alternative: Predict always taken
	- Assume that jump will always happen
	- Always fetch target instruction

#### Better Branch Prediction:
- Predict by Opcode:
	- Some instructions are more likely to result in a jump than others
	- Can get up to 75% success
- Taken/Not taken switch
	- Based on previous history
	- Good for loops 

#### 2 bit Predictor:
- 2 bit code for recording branch behaviour
- Records using a state machine

![[Pasted image 20241222223426.png]]
  
  
  
#### 32 and 64 bit Intel CPU:
- Branch prediction is very sophisticated
- Dynamic data flow analysis (helps out of order)
- Speculative execution (beyond branch)
- Retirement unit looks to see what can complete 


#### Summary:
- Pipelines are designed to complete an instruction each clock
- Branches can cause wasted effort in pipeline stalls as the wrong instructions are being worked on
- Branch prediction units can be > 90% accurate which improves real-world speed.
  
  
  
# References