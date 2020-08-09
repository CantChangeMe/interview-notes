# Performance tuning with hibernate

## Measure performace then tune it

## Created indexes

## Caching
<pre>
        1.First level cache (enabled by default)
            Within the transaction
        2.Second level cache (ehcache)
            Across multiple transactions
        3.Distributed cache (hazelcast)
            Across multiple instances of the application
            
</pre>
## Lazy vs Eager fetch
    
## N+1 Problem
<pre>
    Happens when we have relationships for Example Course can have multiple students
    Fixes:
        1.Using entity graph
             EntityGraph<Course> entityGraph = em.createEntityGraph(Course.class);
             entityGraph.subgraph("students");
             List<Courses> em.createNamesQuery("query_get_all_courses",Course.class)
             .setHint("javax.persistence.loadgraph",entiryGraph)
             .getResultList();    
                 
        2.Using Join Fetch
            Just use "Join Fetch" in query
</pre>            
