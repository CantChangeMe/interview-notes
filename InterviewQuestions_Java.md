# Java interview questions:

##### 1.How to decide young generation and old generation size for your application?
   It depends on nature of application.
   If you have lots of temporary objects then there will be lot of minor gc. 
   You can provide arguments **XX:NewRatio=1** to distribute 50% to young generation and 50% to old.
   By default, **NewRatio=2 hence young Generation is 1/3** of total heap.
   Similarly, If you have too many long-lived objects, then you might need to increase the size of tenure space by putting high value of NewRatio.
   
##### 2.Garbage Collection in java
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
   
   
##### Garbage Collection Algorithms?
   **serial collector**
   It uses single thread to perform all the garbage collection and is suitable for basic application with single processor machines.
   
   **Parallel collector**
   It uses multiple CPUs to perform garbage collector. While serial collector uses 1 thread to perform GC, parallel GC uses several threads to perform GC and it is useful when        there is enough memory and good number of cores.
   
   **Concurrent MS(Mark swwep GC)** 
    Concurrent collector performs garbage collection with application threads. It is useful for applications which have medium to large datasets and require quick response time.
