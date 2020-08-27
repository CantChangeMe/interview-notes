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

