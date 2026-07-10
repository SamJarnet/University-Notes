2026-04-30 19:06

Status:

Tags: [[Computer Systems II]]


# Real-Time Scheduling


#### Real-Time Deadlines
- Tasks have deadlines
- Tasks can be periodic or aperiodic 
- Task duration can be constant or not
	- depends on input data
- Deadline
	- The latest time by which a task has to be completed
- Often require predictable behaviour - guarantees

#### CPU Utilisation $U$ 
- $U = c_{total} - c_{idle} \leq 1$ 
- $c_{total}$  = total CPU time available (100%)
- $c_{idle}$ = fraction of CPU time spent in idle task or sleeping

#### Assumptions for Analysis
- Tasks are periodic 
	- convert aperiodic tasks by polling
	- we do this by checking periodically whether the priority task needs doing, if it doesn't just return, if it needs doing, we do it.
- the deadline for a task is its next invocation
	- you might want to bound things like this on a higher schedule
- context switches take no time
	- leave some margin in duration and deadline 


#### Load from Set of Periodic Tasks
-  $U = c_{total} - c_{idle} \leq 1$ 
- Given a set of tasks $T_1, ..., T_n$ with periodicity $p_i$ and fixed CPU time $c_i$ for $T_i$ the utilisation is 
	![[Pasted image 20260430191855.png]]

#### Schedulability
- Requirement: All tasks meet their deadlines all the time
	- this is why we use worst case times for CPU time 
- A Real time system is schedulable if 
	![[Pasted image 20260430192206.png]]
- Assuming periodic times, with the next invocation as deadline and no overhead for context switching
- If it is not schedulable something needs to change, more CPU power etc. It isn't enough to say just increase the periods.
- If it is larger than 1 it could crash or miss deadlines


#### Simple Case
- All tasks can finish within the period of the most frequent task -> Static scheduling possible: use a table to assign time slots to tasks 
	![[Pasted image 20260430192824.png]]

#### Priority
- Fixed (static) priority
	- assigned at compile time 
- Dynamic priority 
	- changes during runtime 
- If you can, use fixed priority as its just simpler

#### Fixed priority scheduling 
- Simple
	- Code (and changes) relatively easy to verify
- Well understood 
	- Confidence in behaviour
- Optimal fixed priority scheme: Rate Monotonic Scheduling 

#### Rate Monotonic Scheduling 
- Requirements:
	- Tasks are independent
		- no blocking for each other
	- Tasks have fixed CPU requirement
		- if you use worse case then this is always true
	- Free context switching 
	- Deadline is task period
- If the conditions for RMS are met, then it is optimal to assign fixed priorities according to the period:
- Most frequent task has the highest priority:
	- Guaranteed scheduling for:
		![[Pasted image 20260430194020.png]]
	![[Pasted image 20260430194037.png]]
- If $U$ is greater, that doesn't mean that we can't do rate monotonic scheduling it just means its not guaranteed in theory (maybe periods are harmonic (multiples of each other))
- prime number periods will likely cause it to be greater as there will always be some remainder

#### RMS Priority
- The priority in RMS is directly derived from the frequency of the task - and has nothing to do with the importance of the task
	![[Pasted image 20260430194955.png]]

#### RMS is optimal for fixed priorities
 - Use RMS, your own priority assignments cannot outperform it 
 - What if your task set does not satisfy the $U$ bound?
 - To guarantee scheduling for any task set that satisfies the conditions the bound has to assume a worst-case task set
	 - your task set may still be RMS schedulable
	 - but you don't get the guarantee that it is 
	 - requires analysis of specific task set

#### Wasting 30% of the CPU time?
- Run non-real time tasks as low priority in remaining CPU time 
	- UI things potentially
- Optimise task periods to achieve a regular execution pattern
	- make the task set regular and there will be less remainder time on tasks and can fit more in

#### Harmonic Task Sets 
- Every task period is a multiple of any higher priority task
	![[Pasted image 20260504152311.png]]
- You can make periods shorter but not longer
- You can now use up to 100% of the CPU
- Emphasis on any higher priority task so 15 30 and 45 would be wrong 
- when making the task set harmonic, the periods decrease so U will increase so you may need to recheck if it is too high.

- If possible make your task sets harmonic and schedule with RMS 
- RMS can reach 100% utilisation with harmonic task sets
- Harmonic task sets are easy to analyse
	- regular execution pattern
- Note: shorter deadlines may be better
	- decrease periods to make harmonic

#### RMS issues to consider
- What happens in RMS scheduling in an overload situation?
	- Is stable
	- Should not happen
	- It will fail the deadlines of the least priority tasks first
- Are the assumptions made for RMS analysis realistic?
	- The independence of tasks is difficult 
	- Shared resources
- Deadlines can be used instead of periods
	- Useful if deadlines are earlier than next period
- If all else fails and you can't do DPS for some reason you may need to improve a tasks speed or CPU speed

## Dynamic Priority Scheduling 

#### Earliest Deadline First
- Is a high utilisation possible with non-harmonic task sets?
	- Dynamic change of priority
	- Run most urgent task first
	- higher complexity in the scheduler
	- Utilisation up to 100% possible
	- With an without preemption

#### EDF
- ![[Pasted image 20260504154723.png]]
- Scheduler is more complicated
- Scheduler has more overhead
- Can handle changing importance of tasks 
- Can accommodate new tasks at runtime 
- Can handle variable execution times
- Not stable under overload
- EDF is optimal 
# References