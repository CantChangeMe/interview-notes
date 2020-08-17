## Multithreading interview questions:
##### 1.What will happen in case of below program?
  public class SynchronizedCounter {
      private int c = 0;

      public synchronized void increment() {
          c++;
      }
      
      public synchronized int value() {
          return c;
      }
  }
  
  **1.** First, it is not possible for two invocations of synchronized methods on the same object to interleave. When one thread is executing a synchronized method for an object,       all other threads that invoke synchronized methods for the same object block (suspend execution) until the first thread is done with the object.
  **2.** Second, when a synchronized method exits, it automatically establishes a happens-before relationship with any subsequent invocation of a synchronized method for the same      object. This guarantees that changes to the state of the object are visible to all threads.
   
 
##### What is Synchronization?
  Synchronization is ability to restrict access to shared resource to only one thread. When two or more threads need access to shared resource, there has to be some mechanism such   that shared resource will be used by only one thread. The process by which we can achieve it is called Synchronization.

  You can achieve Synchronization using two ways.

  ###### synchronized method
  ###### synchronized block
  
##### How many types of locking are there in Java?
  There are two types of locking in java.

  ###### Object level locking
  ###### Class level locking
  
  **Object level locking:**
    Object level locking means you want to synchronize non static method or block so that it can be accessed by only one thread at a time for that instance. It is used if you      want to protect non static data.
    You can achieve Object level locking by follow
  
  **Class level locking:**
   Class level locking means you want to synchronize static method or block so that it can be accessed by only one thread for whole class. If you have 10 instances of class,        only   one thread will be able to access only one method or block of any one instance at a time. It is used if you want to protect static data.

  
    
