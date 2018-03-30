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
| Unsynchronized counter  |                    |                 |
| Using ReentrantLock     |                    |                 |
| Syncronized method      |                    |                 |
| AtomicLong for total    |                    |                 |

## 1. Using unsynchronized counter object

answer the questions (1.1 - 1.3)

	1.1) The total should be 0 (add & subtract).
		 It isn't always the same because counter is unsynchronize object.
		 There are 2 processes that run in the same time(thread0 and thread1). 
		 When the CPU computes the result, it doesn't have the same pattern 
		 to compute the result in everytime. So, the total of counter that be used 
		 in the processes will not the real total of thread0 or thread1.
		 
	1.2) (1) -> 0.017682 sec
		 (2) -> 0.017732 sec
		 (3) -> 0.016559 sec

## 2. Implications for Multi-threaded Applications

How might this affect real applications?  
	
	There are many customers deposit, withdraw, or transfer money in the same time
	and it will run with the error results that be called from the counter.
	
## 3. Counter with ReentrantLock

answer questions 3.1 - 3.4

	3.1) The most results are possitive number and it isn't always 0.
		 (1) -> 0.207213 sec
		 (2) -> 0.210054 sec
		 (3) -> 0.206850 sec
		 
	3.2) The results are differnt from problem1 because of Lock that use with the counter.
		 It makes the threads call the total after another one set the new total value of counter.
		 So, it doesn't have case that the threads call the same total value in the same time.
		 
	3.3)
	
	3.4)

## 4. Counter with synchronized method

answer question 4

## 5. Counter with AtomicLong

answer question 5

## 6. Analysis of Results

answer question 6

## 7. Using Many Threads (optional)

