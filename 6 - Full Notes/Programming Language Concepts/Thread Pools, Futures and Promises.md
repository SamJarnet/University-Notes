2026-04-28 20:46

Status:

Tags: [[Programming Language Concepts]]


# Thread Pools, Futures and Promises

#### Thread Pools
- The business of deploying tasks concurrently and managing the underlying OS threads that execute the tasks need not be tied together
- The traditional Java approach of new Thread().start() exemplifies this method of using threading.
- What if we separate the creation of threads from the deployment of tasks 
- We could create a separate object that manages creation, destruction, priority and scheduling etc.
- This could be a library implementation tailored for the particular architecture we are using.
- This then leaves the programmer free to concentrate on just creating the tasks and submitting them for execution.

#### Thread Pools in Java
- In java.util.concurrent we have the interface Executor that contains the single method void execute (Runnable task) 
	- This method assigns the task to a thread depending on the underlying implementation and causes it to be executed at some point 
- Implementations of a sub-interface of this called ExecutorService provides what we think of as a Thread Pool.
- Such implementations contain a suite of methods for submitting jobs to the ExecutorService, which will then be mapped to a system thread for execution
- The particular way a thread is mapped to a system thread depends on the implementation. E.g. for java:
	![[Pasted image 20260428212648.png]]

#### Pros and Cons of Thread Pools
- Removes the onus of thread management from the user
- Removes the overhead of thread creation and start time whenever a thread is reused 
- Efficient and correctly started thread management code

- Risks of deadlocks in fixed size pools that are too small
- Risk of excess overhead for thread pools that are too large - resource thrashing 
- Risk of thread leakage if a thread throws an exception that is not handled properly - it can be removed from the thread pool and effectively shrinks the size of the pool

- Choosing an appropriately size thread pools is important 

#### The submit method
- An interesting method in ExecutorService is submit (Runnable task) 
- This method is similar to execute (Runnable task) but with the key difference that submit method provides a mechanism for determining when the task has completed
- It does this by returning a special object that tracks progress of the task in the thread pool
- This special object can also be used to cancel execution of the task after the task has been deployed but not yet completed
- The special object is what is known as a Future

#### Asynchronous Programming 
- A common concurrency idiom is that of offloading some task to another thread whilst the main thread continues execution. 
- When the other thread task completes the main thread needs signalling somehow that the work is done 
- This is not always easy:
	- Callbacks can be used - the other thread calls a "finished" method on the main thread's object that is ready to process callbacks - but these create very messy code 
	- Where multiple threads or coroutines are used the completion signal must be sent to the correct waiting thread. not all threading and coroutine libraries support this 
- The main thread could just offload the task and bind the result of the task to some placeholder object which the result will be stored
- If we could test for the presence of a result, wait on it, and fetch the result from the placeholder then we could just program our main thread without worrying too much about the asynchrony.
- These placeholder objects are what is knows as a Future

#### Future in Java
- java.util.concurrent.Future$<$v$>$
- The Future$<$v$>$ interface in java lists the following methods:
	![[Pasted image 20260428213742.png]]
- The first of these allows a Future task to be cancelled after submission but before completion. The boolean flag determines whether to allow a currently executing thread to be interrupted or not.
- The get methods probe the Future to see whether the task has completed yet, if not then the calling thread will wait until it has (or is cancelled)
- The get method can be called with a timeout to avoid risks of deadlock.

#### The Future Idiom
- Creating Futures in Java is typically done by calling submit on a thread pool.
- You can create Future$<$v$>$ objects directly by using the FutureTask class that accepts a Callable$<$v$>$. this class implements Runnable and thus instances can be passed to execute (Runnable task) in a thread pool:
	![[Pasted image 20260428214139.png]]


#### Promises 
- Futures are read only 
- The asynchronous task to which a Future is attached is responsible for completing the Future with a value (or failing it with an exception).
- The client code that handles the Future object cannot complete it 
- Occasionally it is useful to have code that complete a Future by writing a value into it but java.util.concurrent.Future has no capacity for that
- A write-once container that behaves like a Future is known as a Promise
- The idea is that Futures will be completed at some point by another task, a Promise is something you must complete.
- A promise can be used to create a Future that can be given to another task - writing to the Promise completes that Future.
- In java, Promises are implemented by a complicated class called CompleteableFuture

#### Futures in Scala 
- The future class in Scala behaves much like Java
- Blocking on a Future in Scala is discouraged; asynchronous callbacks are the preferred option 
- Support for asynchronous callbacks is provided in the form of "on complete" 
	![[Pasted image 20260429120130.png]]
- Note the two cases used for successful completion and failure of the Future.

#### Promises in Scala 


- Each instance of the Promise class in Scala has an associated Future instance
- This is accessible by via the future property of the Promise 
- To write to a Promise and complete its associated Future we use the "success" primitive
- Consider this Producer/Consumer example using Promises and Futures
	![[Pasted image 20260429120422.png]]

#### Combining Futures
- By using promises we can combine Future values in interesting ways 
- We need to be able to both read and write Future values in order to do this so Promises are essential for such constructions
- Consider this example in which we create a Future from two possible Futures by completing with whichever Future value completes first.
	![[Pasted image 20260429120713.png]]


#### Async/Await 
- An issue with the way that java supports Futures is that the get method is blocking:
	- future.get() blocks the calling thread when the future is not complete
- An issue with the way that Scala supports Futures is that callbacks need separate handling code that is not inline with the control flow where a value is needed.
- What would be better is if we could access values from a Future in the style of a get() but not have it block the thread if the Future isn't complete
	- If the value is not ready - the function could suspend, like a coroutine - but not block the underlying thread.
- This is the idea of the concept of async/await

#### Async / Await Implementations
- One way of thinking of async/await is simply as a tidy way to use coroutines
- Example in Kotlin:
	![[Pasted image 20260429121123.png]]
	- Gere the main thread blocks while the service call computes
	- And a call-back function is passed to process the result 
- If we refactor that using an async block of code:
	![[Pasted image 20260429121230.png]]




# References