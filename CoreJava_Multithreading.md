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
  
