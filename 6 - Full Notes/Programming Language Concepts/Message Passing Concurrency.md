2026-04-27 10:52

Status:

Tags: [[Programming Language Concepts]]


# Message Passing Concurrency

#### Message Passing
- Concurrent Programming is hard
- This stems from the difficulties arising in the shared memory concurrency model and the issues with:
	- Race conditions, critical sections, mutexes, deadlock, cache visibility, instruction reordering etc.
- A fundamental principle of concurrent programming is that threads must communicate by sending some sort of messages to each other
- What if we built our concurrency model and programming languages around this principle instead?
- Assuming an efficient and correct implementation of a mechanism by which we can send messages from one thread to another, then concurrent programming can be reduced to a series of thread creation and message passing instructions.

#### Advantages of Message Passing
- If we give up on shared memory concurrency and use message passing instead, then we:
	- don't have to worry about critical regions and mutex locks 
	- run less risk of deadlock as we aren't necessarily holding locks 
	- avoid problems with cache visibility as we know which thread is the intended recipient of the message
- When programming for a distributed system, we have a number of processes running on different machines trying to communicate 
	- Shared memory is obviously not an option in this scenario so message passing is typically used here
	- By using message passing for concurrent programming too we can use a single model that scales from single machine, to multi/many core to distributed systems.
- Message passing systems have well established interfaces (e.g. MPI) and well studied theory 

#### Disadvantages of Message Passing 
- With these advantages why is the predominant model still based on shared memory?
	- Harder to ensure a global consensus 
	- Speed
		- shared memory concurrency, with architectural support in the form of test and set lock instructions is very fast when compared to higher level implementations of message queues 
	- Could speed up to shared memory levels with more research

#### Synchronous and Asynchrony 
- Synchronous message passing (sender blocks until receive is ready) is popular for hardware design languages and is easier to program with but is difficult (and at worst impossible) to arrange in a distributed system.
- Asynchronous message passing (sender does not block, messages are buffered) is the popular choice for distributed applications 
- Programming for asynchronous systems can be difficult:
	- Typically the idiom is to send a message and set up a receiver for a callback when the message is received 
	- Callbacks appear "non-linearly" in the program flow and do not help with maintainability and debugging
	- The flow messages controls the program flow

#### Example Producer/Consumer
- Consider the following Java-like code showing a Producer/Consumer implementation that uses asynchronous message passing to communicate in a bounded way.
	![[Pasted image 20260427110827.png]]

#### Channels 
- In the previous example we assumed a single point through which to send and receive messages
- This does not scale well for many threads
- In practice, messages are 
	- a handshake between just two threads
	- group multicast between many threads
	- broadcast to all threads on the system
- For the former two at least, in order to achieve this it is common to use a naming scheme to identify a channel of communication. Sending and receiving of messages is done via a named channel.
- A common alternative approach is to implement channel objects, sometimes with separate endpoints for just sending or just receiving messages.

#### The Actor Model
- A model of concurrent programming inspired from ideas in physics in quantum mechanics and general relativity.
- Most languages have Actor libraries rather than direct language support.
- The starting point is that all computation is performed by actors.
- Actors have a thread of control
- Actors do not share memory
- Actors have unique addresses to which they can be sent messages 
- Actors have a "mailbox" that acts as a FIFO queue for incoming messages 
- Actors can send messages, or values, to other actors and receive messages from their own mailbox.

#### Actor Messages
- Actor messages consist of values, these can be typed or untyped 
- Values can include the address of other actors, this means the underlying communication topology is dynamic.
- In response to receiving a message, an actor can 
	- Send a finite number of messages to other actors
	- Create, or spawn, a finite number of new actors 
	- Change its own behavioural state
- Actors communicate "locally" this means actors only send to other actors for which they either:
	- already know the actor's address
	- have already received the actor's address in the previous message
	- are the creator of the actor
- It may of course be possible to "guess" addresses to send to but a decent address allocation algorithm should avoid this

#### Actor example 1
- There are no messages sent or received but new actors are spawned
- The instance of tut14 has en entry point of start(), this spawns two ore instances of tut14 with different entry points and parameters. 
	![[Pasted image 20260427112306.png]]

#### Actor example 2 
- Involves message passing.
	![[Pasted image 20260427112458.png]]


#### Hierarchical Actors 
- Another feature of some Actor implementations is the ability to group Actors in a hierarchy. 
- Each actor has a unique parent Actor who created it and the parent Actor supervises various features of the behaviour.
- For example, the parent can delegate actions to its sub-Actors. 
- Error handling in Actors can also be handled hierarchically:
	- Failures (exceptions) in lower Actors can be passed up to higher Actors in the hierarchy if not handled.
	- Handling can be specified as a:
		- "One for One" strategy - handler applies to failed children only
		- "All for One" strategy - handler applies to all children
	- Possible Handler actions to an Actor are: 
		- Resume, Restart, Stop, Escalate 

# References