## Motivation  : Why we need threads?
  * Responsiveness
  * Performance

Example of poor responsiveness
  * Waiting for customer support
  * Late response from a person
  * No feedback from an application
  
Responsiveness is particularly critical in applications with User Interface.

## Single Threaded Application Process
<p align="center">
  <img width="650" height="300" src="https://user-images.githubusercontent.com/8223432/91295134-3a84c580-e7b8-11ea-9c26-248b3d3ee47f.PNG">
</p>

## Multi Threaded Application Process
<p align="center">
  <img width="650" height="300" src="https://user-images.githubusercontent.com/8223432/91295211-5a1bee00-e7b8-11ea-8cdb-2194e77054ca.PNG">
</p>

## Motivation for multithreading
  * Responsiveness is achieved by concurrency
  * Performance is achieved by parallelism
  
## What threads contain
  * Stack
  * Instruction pointer
  
## What threads share
  * Files
  * Heap(Data)
  * Code
  
## Context switch
<p align="center">
  <img width="650" height="300" src="https://user-images.githubusercontent.com/8223432/91296876-f5ae5e00-e7ba-11ea-8b6d-d1fd7a4bc0e6.PNG">
</p>
  * Too many threads - Thrasing ,spending more time in management that doing real productive work.
  * Threads consume less resources than processes.Context switch between threads from the same process is cheaper.
  
## Thread scheduling
  * First come first server
  * Shortest job first
  * Time slices -Epochs
    
## Thread.sleep(10000)
  This method instructs operating system not to schedule current thread until that time passes.
  During that time this thread is not consuming any CPU time.

## Catching exception in a thread
  If some unchecked exception is thrown from a thread and you want to recover from that exception you can use
  below setUncaughtExceptionHandler on the threads
  ```Java
          thread.setUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
            @Override
            public void uncaughtException(Thread thread, Throwable throwable) {
                System.out.println("You are saved now."+ throwable.getLocalizedMessage()+"Thread "+Thread.currentThread().getName()+" was misbehaving.");
            }
        });
  ```
## Thread termination - Why and when?
 * Thread comsumes resources like mwmory ,kernel resources and CPU cycles.   
 * If a thread has finished work , but application is still running, we want to clean up the thread's resources.
 * If a thread is misbehaving and we want to stop it.
 * The application will not stop as long as one thread is still running.

## Thread.interrupt()
* If a thread is executing a method that throws **InterruptedException** when it gets interrupted.//Thread.sleep(10000000000) throws InterruptedException
* If the thread we are trying to interrupt is handling interrupt signal explicitly.

## How to stop a thread using Thread.interrupt()?
* When we are using a method that responds to interrupt signal.
```Java
1.
public class InterruptedExceptionTest {
    public static void main(String[] args) {
        Thread thread = new Thread(new BlockingTask());
        thread.start();
        thread.interrupt();
    }
}

2.public class BlockingTask implements Runnable{
    @Override
    public void run() {
        try {
            System.out.println("BlockingTask.run");
            Thread.sleep(600000);
            System.out.println("BlockingTask.run2");
        } catch (InterruptedException e) {
            System.out.println("Thread is exiting after being interrupted.");
        }
    }
}
```
* Or checking our code and handling exceptions ourselves.
```Java
 1. public class Main2 {

    public static void main(String[] args) {
        Thread thread = new Thread(new LongComputationTask(new BigInteger("200000"), new BigInteger("100000000")));

        thread.start();
        thread.interrupt();
    }
  }
 2. private static class LongComputationTask implements Runnable {
        @Override
        public void run() {
            System.out.println(base + "^" + power + " = " + pow(base, power));
        }

        private BigInteger pow(BigInteger base, BigInteger power) {
            BigInteger result = BigInteger.ONE;

            for (BigInteger i = BigInteger.ZERO; i.compareTo(power) != 0; i = i.add(BigInteger.ONE)) {
                if (Thread.currentThread().isInterrupted()) {
                    System.out.println("Prematurely interrupted computation");
                    return BigInteger.ZERO;
                }
                result = result.multiply(base);
            }

            return result;
        }
   }
```
## Another way to stop blocking our application by a thread is to set the thread as demon thread.

## The Thread.join() Method
#### public final void join() throws InterruptedException
Waits for this thread to die.

When we invoke the join() method on a thread, the calling thread goes into a waiting state. It remains in a waiting state until the referenced thread terminates.

* The join() method may also return if the referenced thread was interrupted.  In this case, the method throws an InterruptedException.
* Finally, if the referenced thread was already terminated or hasn't been started, the call to join() method returns immediately.
```Java
Thread t1 = new SampleThread(0);
t1.join();  //returns immediately
```

## Thread.join() Methods with Timeout
The join() method will keep waiting if the referenced thread is blocked or is taking too long to process. This can become an issue as the calling thread will become non-responsive. To handle these situations, we use overloaded versions of the join() method that allow us to specify a timeout period.

#### public final void join(long millis) throws InterruptedException
Waits at most millis milliseconds for this thread to die. A timeout of 0 means to wait forever.
* Timed join() is dependent on the OS for timing. So, we cannot assume that join() will wait exactly as long as specified.

## 4. Thread.join() Methods and Synchronization
This means that when a thread t1 calls t2.join(), then all changes done by t2 are visible in t1 on return. However, if we do not invoke join() or use other synchronization mechanisms, we do not have any guarantee that changes in the other thread will be visible to the current thread even if the other thread has completed.

## What are ways for inter-thread synchronization?
* wait()
* notify()
* join()

## Peformance Analysis -Latency vs Threads
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91524521-10004d00-e91d-11ea-801f-a9db83a6c2ce.PNG">
</p>

*  we can improve the performance and get a significant speed up if the problem can be partitioned
into multiple subproblems and is performed by multiple threads.
* We proved that having more threads than cores is counterproductive for a problem that involves only
computations and no blocking calls.
* So the problem we want to partition needs to be large enough to make the effort worthwhile.


## Inherent cost of parallelization and and aggregation is caused by:
* Breaking tasks into multiple tasks.
* Thread creation and passing tasks to threads.
* Time between thread start and thread getting scheduled.
* Time until last thread finishes and signals.
* Time until the aggregating thread runs.
* Aggregation of the suresults into a single artifact.


## Thread pooling:
* Thread pooling is nothing more than just creating the threads once and reusing them for future tasks
instead of recreating the threads each and every time from scratch.
* Once the threads are created they sit in the pool and the tasks are distributed among the threads through a queue each thread is taking tasks from that queue whenever that thread is available.
* If all the threads are busy the task search is going to stay in the queue and wait for a thread to become available if we keep the threads well busy and utilized and we keep feeding tasks into the queue we

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91526942-61f7a180-e922-11ea-86c9-5ca12bca5e59.PNG">
</p>

## Thread pool -Implementation
* JDK comes with a few implementations of thread pools
for example , Fixed Thread Pool Executor

* Fixed Thread Pool Executor
```Java
        int noOfThreads =4;
        Executor executor = Executors.newFixedThreadPool(noOfThreads);

        Runnable task = ()-> System.out.println("FDf");
        executor.execute(task);
```

## Throughput
* By serving each task independently on a different thread we can improve the performance by a factor of n where 
* #N  == #Threads == #Cores
* Performace(xN)
* By maintaining a constant number of threads ,we eliminate the need to recreate the threads.

## Throughtput test using JMeter

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91530155-442d3b00-e928-11ea-8d3c-7ec6f25da499.PNG">
</p>

## Peformance Analysis -Throughput

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91530775-5196f500-e929-11ea-906b-28196f14cda4.PNG">
</p>

