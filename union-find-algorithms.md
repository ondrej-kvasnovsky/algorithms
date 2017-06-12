# Union-Find Algorithms

### Scientific method

Steps to develop a usable algorithm using scientific method:

1. Define the problem.
2. Find an algorithm to solve it.
3. Fast enough?
4. If not, figure out why.
5. Find a way to address the problem.
6. Iterate until satisfied.

### Dynamic connectivity

Given set of N objects we support two operations:

* Union command, that connects two objects
* Find connected objects command, that fins if two objects are connected

![](/assets/Screen Shot 2017-06-11 at 2.49.06 PM.png)Another connectivity example. ![](/assets/Screen Shot 2017-06-11 at 8.30.03 PM.png)

### Modeling the connections

![](/assets/Screen Shot 2017-06-11 at 9.41.54 PM.png)If we connect 1 and 2, we need to recreate groups of connected points.![](/assets/Screen Shot 2017-06-11 at 9.44.00 PM.png)

### Quick-Find - eager approach

The elements are connected if the have the same number in an array. 

![](/assets/Screen Shot 2017-06-11 at 9.51.16 PM.png)

### Union

In order to union \(connect the points\) we need to change all from id\[p\] to id\[q\].

![](/assets/Screen Shot 2017-06-11 at 9.52.06 PM.png)

### 









