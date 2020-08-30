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

## Peformance Analysis -Throughput and Latency

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91531115-df72e000-e929-11ea-9227-a8e8e1918a47.PNG">
</p>

## Stack's properties
* All the variables passed on the stack belong to a particular thread and other threads have no access to them
* The stack is allocated statically when the thread is created.
* Its size is fixed and cannot change at runtime
* We have to be very careful not to nest too many method calls because if the calling hierarchy is too deep we may run out of
the memory allocated for that stack and get a stack overflow exception that's particularly a big risk when running a recursive methods.

## What is stored in Heap?

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91557518-39879b80-e952-11ea-8e05-d18ee0b737c1.PNG">
</p>

##  Heap Memory management

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91557800-c6caf000-e952-11ea-94e7-e5cfa3b66cd6.PNG">
</p>

## What are stored where?

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91557800-c6caf000-e952-11ea-94e7-e5cfa3b66cd6.PNG">
</p>

<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91556740-d9dcc080-e950-11ea-85de-95a62feeecf8.PNG">
</p>

## Everything outside the process is also shared between threads

## Why do we need to share resources?
* Text Editor (IU Thread , **Document saver thread**) // Here **document data structure** is shared between UI thread and Document thread.
* Work queue ( tasks within the **Work queue** are shared between the **Worker Threads**)
* Database microservices (**Database connections** are shared between the **Request Threads**)

## How do solve Concurrency Challaenges:
#### Synchronized - Monitor  // By putting sychronized keyword in front of method name.
* We use it is by declaring one or more methods in a class using the synchronized keyword 
* when multiple threads are going to try to call these methods on the same object of this class only one thread would be able to execute either of those methods notice
* that if **thread A** is executing method one **thread B** is deprived from executing both method one and Method two that's because the **synchronized is applied per object** the term for that is called a **monitor**

```Java
public class ClassWithCriticalSections{
  
  public sychronized void m1(){
  //Thread A executing, Thread B can not access both m1 and m2 as 
  }
  
  public sychronized void m2(){
  }
  
}
```
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91627028-bd349d00-e9d1-11ea-939e-498a09d35171.PNG">
</p>

#### Synchronized - Lock // Using aroung a block of code
 Achieved by using synchronized keyword at block level.
* Synchronized block is **Reentrant** 
* That is if **thread A** is accessing a synchronized method while already being in a different synchronized method or block it will be able to access that synchronized method with no problem.
* Basically a thread cannot prevent itself from entering a critical section

```Java
    public class InventoryCounter {
        private int items = 0;

        Object lock = new Object();

        public void increment() {
            synchronized (this.lock) {
                items++;
            }
        }

        public void decrement() {
            synchronized (this.lock) {
                items--;
            }
        }

        public int getItems() {
            synchronized (this.lock) {
                return items;
            }
        }
    }
```
 
## Give the example of Atomic operations.
#### All reference assginments are atomic.
```Java
Object a = new Object();
Object b = new Object();
a = b; // atomic
```
#### Getters and setters are atomic
#### All assigments to primitive types are safe except for long and double.
* we can safely read and write to below types **without the need to synchronize **:

int
short
byte
float
char
boolean 

#### long and double assignments are are not atominc because the 64 bits long and one write can on left 32 bits and anothe write could be on right 32 bits.

#### Assignments to long and double when declared volatile are atomic.
volatile double a = 1.0;
volatile double b = 2.0;
a = b; //atomic

#### class in the package java.util.concurrent.atomic

## Atmomic operations use case:
```Java
public class AtmomicTestRunner {
    public static void main(String[] args) {
        Metrics metrics = new Metrics();

        BusinessLogic businessLogicThread1 = new BusinessLogic(metrics);

        BusinessLogic businessLogicThread2 = new BusinessLogic(metrics);

        MetricsPrinter metricsPrinter = new MetricsPrinter(metrics);

        businessLogicThread1.start();
        businessLogicThread2.start();
        metricsPrinter.start();
    }

    public static class MetricsPrinter extends Thread {
        private Metrics metrics;

        public MetricsPrinter(Metrics metrics) {
            this.metrics = metrics;
        }

        @Override
        public void run() {
            while (true) {
                try {
                    Thread.sleep(4);
                } catch (InterruptedException e) {
                }

                double currentAverage = metrics.getAverage();

                System.out.println("Current Average is " + currentAverage);
            }
        }
    }

    public static class BusinessLogic extends Thread {
        private Metrics metrics;
        private Random random = new Random();

        public BusinessLogic(Metrics metrics) {
            this.metrics = metrics;
        }

        @Override
        public void run() {
            while (true) {
                long start = System.currentTimeMillis();

                try {
                    Thread.sleep(random.nextInt(2));
                } catch (InterruptedException e) {
                }

                long end = System.currentTimeMillis();

                metrics.addSample(end - start);
            }
        }
    }

    public static class Metrics {
        private long count = 0;
        private volatile double average = 0.0;

        public synchronized void addSample(long sample) {
            double currentSum = average * count;
            count++;
            average = (currentSum + sample) / count;
        }

        public double getAverage() {
            return average;
        }
    }
}
```

## Race condition
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91637469-4c6ba000-ea26-11ea-910c-7a9ba40a4092.PNG">
</p>

## Data race
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91637736-2ba44a00-ea28-11ea-8a43-00072ab81abd.PNG">
</p>

## Coarse-grained locking
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91651021-d8241180-eaa4-11ea-89d8-f40a5da65038.PNG">
</p>

## Fine-grained locking
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/91651074-86c85200-eaa5-11ea-851c-0cb5e3363bf7.PNG">
</p>





