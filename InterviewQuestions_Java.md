# Java interview questions:

### 1.How to decide young generation and old generation size for your application?
   It depends on nature of application.
   If you have lots of temporary objects then there will be lot of minor gc. 
   You can provide arguments **XX:NewRatio=1** to distribute 50% to young generation and 50% to old.
   By default, **NewRatio=2 hence young Generation is 1/3** of total heap.
   Similarly, If you have too many long-lived objects, then you might need to increase the size of tenure space by putting high value of NewRatio.
   
### 2.Garbage Collection in java
   JVM Memory is divided into three parts:
   Young and old are part of Heap memory only.
   **Young generation**()
   **Old generation**
   **Metaspace (Perm Gen)**   

   **Young Generation**
   As the name suggests, young generation is the area where newly created objects are allocated.

   When young generation fills up, it cause minor garbage collection aka Minor GC.
   When minor Gcs occurs, dead objects will be removed from young generation.
   If you have lot of dead objects in young generation, Minor GC will be perfomed faster.
   All minor GCs are “stop the world” events, so when minor GCs occurs, application threads will also stop.
   Let’s understand more about how objects are allocated in Young generation.

   **Young generation** is divided into 3 parts.

   **Eden space**
   **Survivor space S0**
   **Survivor space S1**
   
   1.All newly created objects are allocated in eden space.
   2.When Eden space is completely filled with objects then minor GC will occur. All the objects which are not dead or unreferenced will be moved to one of the survivors spaces.    In our case, let’s say all the objects are moved to S0.
   3.When Eden space is filled again, then all the live objects in Eden space andSurvivor space S0 will be moved to Survivor space S1.
   
   4.Once objects are survived multiple cycles of minor GC, they will be moved to old generation. You can control this threshold by MaxTenuringThreshold. The actual tenuring threshold is dynamically adjusted by JVM.
   
   
   **Old generation**
   It is used to hold old long surviving objects
   It is generally larger than the young generation.
   When tenured space is completely filled(or predefined threshold) with objects then Major GC will occur. It will reclaim the memory and free up space.
   Often, Major GCs are slower and less frequent than minor GC.
   
   
### 3.Garbage Collection Algorithms?
   **serial collector**
   It uses single thread to perform all the garbage collection and is suitable for basic application with single processor machines.
   
   **Parallel collector**
   It uses multiple CPUs to perform garbage collector. While serial collector uses 1 thread to perform GC, parallel GC uses several threads to perform GC and it is useful when        there is enough memory and good number of cores.
   
   **Concurrent MS(Mark swwep GC)** 
    Concurrent collector performs garbage collection with application threads. It is useful for applications which have medium to large datasets and require quick response time.
### 4.What is difference between Collection.synchronizedMap(map) and ConcurrentHashMap?
      When you make map thread safe by using Collection.synchronizedMap(map), it locks whole map object, but ConcurrentHashMap does not lock the whole map, it just locks part of       it(Segment).
      
### 5.Differences Between Hashtable and HashMap
   **Synchronization**
   Firstly, Hashtable is thread-safe and can be shared between multiple threads in the application.

      On the other hand, HashMap is not synchronized and can't be accessed by multiple threads without additional synchronization code. We can use Collections.synchronizedMap()       to make a thread-safe version of a HashMap. We can also just create custom lock code or make the code thread-safe by using the synchronized keyword.

      HashMap is not synchronized, therefore it's faster and uses less memory than Hashtable. Generally, unsynchronized objects are faster than synchronized ones in a single           threaded application.
      
   **Null Values**
   Another difference is null handling. HashMap allows adding one Entry with null as key as well as many entries with null as value. In contrast, Hashtable doesn't allow null at      all.
   **Iteration Over Elements**
   HashMap uses Iterator to iterate over values, whereas Hashtable has Enumerator for the same. The Iterator is a successor of Enumerator that eliminates its few drawbacks. For    example, Iterator has a remove() method to remove elements from underlying collections.
   The Iterator is a fail-fast iterator. In other words, it throws a ConcurrentModificationException when the underlying collection is modified while iteratin
   
### 6.When to Choose HashMap Over Hashtable
   We should use HashMap for an unsynchronized or single threaded application.

   It is worth mentioning that since JDK 1.8, Hashtable has been deprecated. However, ConcurrentHashMap is a great Hashtable replacement. We should consider ConcurrentHashMap to    use in applications with multiple threads.

### 7.Difference between HashMap, HashTable ,synchronizedMap and ConcurrentHashMap
<p align="center">
  <img width="750" height="400" src="https://user-images.githubusercontent.com/8223432/90375685-e9c3ed00-e092-11ea-95c8-da3800d5c413.PNG">
</p>

### 8.How to print even and odd numbers using threads in java

### 9.Which design pattern you have used in your project?
   You can name few design patterns such as Singleton, Observer etc. which you might have used in your project.

### 10.What is double level locking in singleton design pattern?
   Double level locking in Singleton design pattern  is used to make it thread-safe.
   
   public static SingletonInstance getInstance(){
      if(instace ==  null){
         synchronized(SingletonInstance.class){
            if(instance == null){
               instance = new SingletonInstance();
            }  
         }
      }
      return instance;
   }
  
  Let’s say two threads(T1 and T2) checked for null and both reached at synchronized (Singleton.class). T1 gets the lock and create instance of Singleton and return. Now T2       enters in a synchronized block, as we have checked for null again, it will not create object again.
    
### 10.Question 2. Does not overriding hashCode() method has any performance implication? (answer)
   This is a good question and opens to all, as per my knowledge, a poor hash code function will result in the frequent collision in HashMap which eventually increases the time    for adding an object into Hash Map.
   From Java 8 onwards though collision will not impact performance as much as it does in earlier versions because after a threshold the linked list will be replaced by a binary      tree, which will give you O(logN) performance in the worst case as compared to O(n) of a linked list. 
