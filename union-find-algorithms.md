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

Cost model: initialize O\(n\), union O\(n\), find O\(1\). Takes n^2 array accesses to process sequence of N union commands on N objects. It is too slow and we can't accept that, quick-find is too slow.

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

### Quick-union - lazy approach

We create tree structure. Before we connect two dots, we need to find root of the dot we want to connect to.![](/assets/Screen Shot 2017-06-11 at 10.54.45 PM.png)Here is an example of a tree with its array.![](/assets/Screen Shot 2017-06-11 at 11.06.36 PM.png)Java implementation:

```
import java.util.Arrays;

class QU {
    private int[] id;

    public QU(int n) {
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
        System.out.println(p + ", " + q);
        int i = root(p);
        int j = root(q);
        id[i] = j;
    }

    public boolean connected(int p, int q) {
        return root(p) == root(q);
    }

    public int root(int index) {
        while (index != id[index]) {
            index = id[index];
        }
        return index;
    }
}

public class QuickUnion {

    public static void main(String[] args) {
        QU uf = new QU(10);
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

Here is the output. 

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
4, 3
[0, 1, 2, 3, 3, 5, 6, 7, 8, 9]
3, 8
[0, 1, 2, 8, 3, 5, 6, 7, 8, 9]
6, 5
[0, 1, 2, 8, 3, 5, 5, 7, 8, 9]
9, 4
[0, 1, 2, 8, 3, 5, 5, 7, 8, 8]
2, 1
[0, 1, 1, 8, 3, 5, 5, 7, 8, 8]
8, 9
[0, 1, 1, 8, 3, 5, 5, 7, 8, 8]
true
false
5, 0
[0, 1, 1, 8, 3, 0, 5, 7, 8, 8]
true
true
```

Quick-union is also slow. Intialize O\(n\), union O\(n\) - but N depends on depth of tree, if tree is too deep, algorithm will perform slowly, find O\(n\).

### Quick-union improvements

#### Improvement 1: Weighting

Link root of smaller tree to root of larger tree.![](/assets/Screen Shot 2017-06-12 at 5.44.55 PM.png)Here is the result of weighting in bigger scope.![](/assets/Screen Shot 2017-06-12 at 5.49.10 PM.png)Java implementation:

```
import java.util.Arrays;

class WQU {

    private int[] indicies; // just to keep visual track of values in arrays
    private int[] ids;
    private int[] weights;

    public WQU(int n) {
        indicies = new int[n];
        ids = new int[n];
        weights = new int[n];
        for (int i = 0; i < n; i++) {
            indicies[i] = i;
            ids[i] = i;
            weights[i] = 1;
        }
    }

    @Override
    public String toString() {
        return Arrays.toString(indicies) + "\n" +
                Arrays.toString(weights) + "\n" +
                Arrays.toString(ids) + "\n";
    }

    public int root(int i) {
        while (i != ids[i]) {
            i = ids[i];
        }
        return i;
    }

    public boolean connected(int p, int q) {
        return root(p) == root(q);
    }

    public void union(int p, int q) {
        System.out.println(p + ", " + q);
        int i = ids[p];
        int j = ids[q];
        if (i == j) {
            // this means they are the same
            return;
        }
        if (weights[i] < weights[j]) {
            ids[i] = j;
            weights[j] += weights[i];
        } else {
            ids[j] = i;
            weights[i] += weights[j];
        }

    }
}

public class WeightedQuickUnion {

    public static void main(String[] args) {
        WQU uf = new WQU(10);
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

Here is the output, observe how values are linked in the array.

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

4, 3
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 2, 1, 1, 1, 1, 1]
[0, 1, 2, 4, 4, 5, 6, 7, 8, 9]

3, 8
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 3, 1, 1, 1, 1, 1]
[0, 1, 2, 4, 4, 5, 6, 7, 4, 9]

6, 5
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 3, 1, 2, 1, 1, 1]
[0, 1, 2, 4, 4, 6, 6, 7, 4, 9]

9, 4
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 4, 1, 2, 1, 1, 1]
[0, 1, 2, 4, 4, 6, 6, 7, 4, 4]

2, 1
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 2, 1, 4, 1, 2, 1, 1, 1]
[0, 2, 2, 4, 4, 6, 6, 7, 4, 4]

8, 9
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 2, 1, 4, 1, 2, 1, 1, 1]
[0, 2, 2, 4, 4, 6, 6, 7, 4, 4]

true
false
5, 0
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 2, 1, 4, 1, 3, 1, 1, 1]
[6, 2, 2, 4, 4, 6, 6, 7, 4, 4]

true
true
```

Initialize O\(n\), union O\(log2n\), connect O\(log2n\).

#### Improvement 2: Path Compression

As we go up through the tree, we flatten the tree by putting the node below the root.![](/assets/Screen Shot 2017-06-12 at 10.20.26 PM.png)Java implementation \(only this line `ids[i] = ids[ids[i]];` has been added to `root` method\).

```
package algorithms;

import java.util.Arrays;

class PathCompWQU {

    private int[] indicies; // just to keep visual track of values in arrays
    private int[] ids;
    private int[] weights;

    public PathCompWQU(int n) {
        indicies = new int[n];
        ids = new int[n];
        weights = new int[n];
        for (int i = 0; i < n; i++) {
            indicies[i] = i;
            ids[i] = i;
            weights[i] = 1;
        }
    }

    @Override
    public String toString() {
        return Arrays.toString(indicies) + "\n" +
                Arrays.toString(weights) + "\n" +
                Arrays.toString(ids) + "\n";
    }

    public int root(int i) {
        while (i != ids[i]) {
            ids[i] = ids[ids[i]];
            i = ids[i];
        }
        return i;
    }

    public boolean connected(int p, int q) {
        return root(p) == root(q);
    }

    public void union(int p, int q) {
        System.out.println(p + ", " + q);
        int i = ids[p];
        int j = ids[q];
        if (i == j) {
            // this means they are the same
            return;
        }
        if (weights[i] < weights[j]) {
            ids[i] = j;
            weights[j] += weights[i];
        } else {
            ids[j] = i;
            weights[i] += weights[j];
        }

    }
}

public class PathCompressionQuickUnion {

    public static void main(String[] args) {
        PathCompWQU uf = new PathCompWQU(10);
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

Here is the output of that program.

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

4, 3
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 2, 1, 1, 1, 1, 1]
[0, 1, 2, 4, 4, 5, 6, 7, 8, 9]

3, 8
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 3, 1, 1, 1, 1, 1]
[0, 1, 2, 4, 4, 5, 6, 7, 4, 9]

6, 5
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 3, 1, 2, 1, 1, 1]
[0, 1, 2, 4, 4, 6, 6, 7, 4, 9]

9, 4
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 1, 1, 4, 1, 2, 1, 1, 1]
[0, 1, 2, 4, 4, 6, 6, 7, 4, 4]

2, 1
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 2, 1, 4, 1, 2, 1, 1, 1]
[0, 2, 2, 4, 4, 6, 6, 7, 4, 4]

8, 9
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 2, 1, 4, 1, 2, 1, 1, 1]
[0, 2, 2, 4, 4, 6, 6, 7, 4, 4]

true
false
5, 0
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 1, 2, 1, 4, 1, 3, 1, 1, 1]
[6, 2, 2, 4, 4, 6, 6, 7, 4, 4]

true
true
```



