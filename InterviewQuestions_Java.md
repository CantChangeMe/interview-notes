# Java interview questions:

##### How to decide young generation and old generation size for your application?
   It depends on nature of application.
   If you have lots of temporary objects then there will be lot of minor gc. 
   You can provide arguments **XX:NewRatio=1** to distribute 50% to young generation and 50% to old.
   By default, **NewRatio=2 hence young Generation is 1/3** of total heap.
   Similarly, If you have too many long-lived objects, then you might need to increase the size of tenure space by putting high value of NewRatio.

