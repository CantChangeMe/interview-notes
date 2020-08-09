
# How to create an Immutable List, Set, and Map in Java?
 ## Before Java8, To create unmodifiableList:
        List<Integer> list2 = new ArrayList<>();
        list2.add(1);
        list2.add(2);
        list2.add(3);
        List<Integer> unmodifiableList =  Collections.unmodifiableList(list2);
        unmodifiableList.forEach(System.out::println);
     
  ## In Java 9 
      List<Integer> list = List.of(1,2,3);
      list.forEach(System.out:println);
      
  
