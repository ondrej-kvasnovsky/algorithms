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

### Java implementation

```
import java.util.Arrays;

class UF {
    private int[] id;

    public UF(int n) {
        id = new int[n];
        for (int i = 0; i < n; i++) {
            id[i] = i;
        }
    }

    @Override
    public String toString() {
        return Arrays.toString(id);
    }

    public void union(int p, int q) {
        int pId = id[p];
        id[p] = id[q];
        for (int i = 0; i < id.length; i++) {
            if (id[i] == pId) {
                id[i] = id[p];
            }
        }
    }

    public boolean connected(int p, int q) {
        return id[p] == id[q];
    }
}

public class UnionFind {

    public static void main(String[] args) {
        UF uf = new UF(10);
        System.out.println(uf);

        uf.union(4, 3);
        System.out.println(uf);

        uf.union(3, 8);
        System.out.println(uf);

        uf.union(6, 5);
        System.out.println(uf);

        uf.union(9, 4);
        System.out.println(uf);

        uf.union(2, 1);
        System.out.println(uf);

        uf.union(8, 9);
        System.out.println(uf);

        boolean connected89 = uf.connected(8, 9);
        System.out.println(connected89);

        boolean connected50_1 = uf.connected(5, 0);
        System.out.println(connected50_1);

        uf.union(5, 0);
        System.out.println(uf);

        boolean connected50_2 = uf.connected(5, 0);
        System.out.println(connected50_2);

        boolean connected49 = uf.connected(4, 9);
        System.out.println(connected49);
    }
}
```

It prints out:

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 3, 5, 6, 7, 8, 9]
[0, 1, 2, 8, 8, 5, 6, 7, 8, 9]
[0, 1, 2, 8, 8, 5, 5, 7, 8, 9]
[0, 1, 2, 8, 8, 5, 5, 7, 8, 8]
[0, 1, 1, 8, 8, 5, 5, 7, 8, 8]
[0, 1, 1, 8, 8, 5, 5, 7, 8, 8]
true
false
[0, 1, 1, 8, 8, 0, 0, 7, 8, 8]
true
true
```



