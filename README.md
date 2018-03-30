## Threads and Synchronization

This lab illustrates the problem of synchronization when many threads are operating on a shared object.  The general issue is called "thread safety", and it is a major cause of errors in computer software.

## Assignment

To the problems on the lab sheet and record your answers here.

1. Record average run times.
2. Write your explanation of the results.  Use good English and proper grammar.  Also use good Markdown formatting.

## ThreadCount run times

These are the average runtime using 3 or more runs of the application.
The Counter class is the object being shared by the threads.
The threads use the counter to add and subtract values.

| Counter class           | Limit              | Runtime (sec)   |
|:------------------------|:-------------------|-----------------|
| Unsynchronized counter  |     10,000,000     |		0.017324    |
| Using ReentrantLock     |     10,000,000     |		0.877877    |
| Syncronized method      |      1,000,000     |		0.286753    |
| AtomicLong for total    |     10,000,000     |		0.212911    |

## 1. Using unsynchronized counter object

answer the questions (1.1 - 1.3)

	1.1) The total should be 0 (add & subtract).
		 It isn't always the same because counter is unsynchronize object.
		 There are 2 processes that run in the same time(thread0 and thread1). 
		 When the CPU computes the result, it doesn't have the same pattern 
		 to compute the result in everytime. So, the total of counter that be used 
		 in the processes will not the real total of thread0 or thread1.
		 
	1.2) Average time is 0.017324 sec
		 (1) -> 0.017682 sec
		 (2) -> 0.017732 sec
		 (3) -> 0.016559 sec

## 2. Implications for Multi-threaded Applications

How might this affect real applications?  
	
	There are many customers deposit, withdraw, or transfer money in the same time
	and it will run with the error results that be called from the counter.
	
## 3. Counter with ReentrantLock

answer questions 3.1 - 3.4

	3.1) It is always 0.
		 Average time is 0.877877 sec
		 (1) -> 0.581792 sec
		 (2) -> 1.041142 sec
		 (3) -> 1.010697 sec
		 
	3.2) The results are differnt from problem1 because of Lock that be used with the counter.
		 It makes the threads call the total after another one set the new total value of counter.
		 So, it doesn't have case that the threads call the same total value in the same time.
		 
	3.3) A ReentrantLock will lock the process that start runing and unlock when the process is done.
	
	3.4) Because every process will unlock when the process is done.

## 4. Counter with synchronized method

answer question 4

	4.1) It is always 0.
		 Average time is 3.148502 sec
		 (1) -> 3.161643 sec
		 (2) -> 3.121490 sec
		 (3) -> 3.162374 sec

	4.2) The results are differnt from problem1 because of using synchronized method.
	
	4.3) When one thread is executing a synchronized method for an object, 
		 other threads that invoke synchronized methods for the same object will 
		 block until the first thread is done with the object.
	
## 5. Counter with AtomicLong

answer question 5

	5.1) Because get() method of AtomicLong get only the current value(the last total that be 
		 set by this process). It likes this method can remember the total of this process.
		 Average time is 0.212911 sec
		 (1) -> 0.207414 sec
		 (2) -> 0.216370 sec
		 (3) -> 0.214949 sec
		 
	5.2) I think it should be used when there are many threads that run in the same time 
		 because using method of Atomic class will be faster and give a correctly result
		 but it's too complicated to use with 1 or 2 threads.

## 6. Analysis of Results

answer question 6

	6.1) Counter with AtomicLong is fastest and Counter with synchronized method is slowest.
	
	6.2) If program has many kinds of functions, I think using Counter with synchronized method 
		 can be applied to the broadest range of problems. Because it's easy to modify or create 
		 synchronized methods to manage the systems and solve the problems. 
		 But if the program has only mathematical functions, I think Counter with Atomic class
		 will be better than synchronized method. Because it can compute the result faster
		 and there are many methods that support the mathemetical calculations.

## 7. Using Many Threads (optional)

