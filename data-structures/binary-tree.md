# Binary Tree

[Binary Tree](https://en.wikipedia.org/wiki/Binary_tree) is a data structure to store hierarchical data where each node has only two leaf nodes.

### Binary Tree using Nodes

The basic building block of binary tree is a node that hold references to left and right nodes.

```
class TreeNode<T> {
    T value;
    TreeNode left;
    TreeNode right;

    public TreeNode(T value) {
        this.value = value;
    }
}
```

Then we create a class that holds the root and provide operations over the binary tree.

```
class BinaryTree<T> {
    TreeNode<T> root;

    public String asString(TreeNode<T> node, int level) {
        if (node == null) return "";
        String value = level + ": " + node.value.toString() + "\n";
        if (node.left != null) {
            value += asString(node.left, level + 1);
        }
        if (node.right != null) {
            value += asString(node.right, level + 1);
        }
        return value;
    }

    public String toString() {
        return asString(root, 0);
    }
}
```

Now we can try to use it and print out how the tree looks like.

```
public class BinaryTreeDemo {

    public static void main(String... args) {
        BinaryTree<String> tree = new BinaryTree<>();
        tree.root = new TreeNode<>("Hello");
        tree.root.left = new TreeNode<>("World");
        tree.root.right = new TreeNode<>("!!!");

        System.out.println(tree);
    }
}
```

Here is the output.

```
0: Hello
1: World
1: !!!
```

### Binary Tree using Array

An alternative to represent trees using node is to keep the values in array. Root element is stored on `0th` position, left is stored on `0th + 1` position and right is stored on `0th + 2` position. If a position of element is i, then left is on `2*i+1` and right is on `2*i+2`. For 0th element, it is `0*2+1` and `0*2+2`. For the left element on `0th` position, it is `2*1+1` and `2*1+2`.

![](/assets/600px-Binary_tree_in_array.svg.png)

Here is an implementation of binary tree that stores and obtains elements from binary tree.

```
class BinaryTreeUsingArray {
    private String[] values;

    BinaryTreeUsingArray() {
        values = new String[10];
    }

    public void setRoot(String value) {
        values[0] = value;
    }

    public void addLeftChild(String value, int root) {
        values[2 * root + 1] = value;
    }

    public void addRightChild(String value, int root) {
        values[2 * root + 2] = value;
    }

    public String toString() {
        return Arrays.toString(values);
    }

    public String asTree() {
        StringBuilder builder = new StringBuilder();
        int stop = 1;
        for (int i = 0; i < values.length; i++) {
            if (values[i] == null) continue;
            if (i < stop - 1) {
                builder.append(values[i]);
                builder.append(" ");
            } else {
                builder.append("\n");
                builder.append(values[i]);
                builder.append(" ");
                stop = stop << 1; // 1, 2, 4, 8, 16, 32 ...
            }
        }
        return builder.toString();
    }
}
```

Here is the output.

```
public class BinaryTreeDemo {

    public static void main(String... args) {
        BinaryTreeUsingArray t = new BinaryTreeUsingArray();
        t.setRoot("A");
        t.addLeftChild("B", 0);
        t.addRightChild("C", 0);
        t.addLeftChild("D", 1);
        t.addRightChild("E", 1);
        t.addLeftChild("F", 2);
        t.addRightChild("G", 2);

        System.out.println(t);
        System.out.println(t.asTree());
    }
}
```

Here is the output.

```
[A, B, C, D, E, F, G, null, null, null]

A 
B C 
D E F G
```

### Balanced & Unbalanced Trees

A balanced binary tree has the minimum possible maximum height \(a.k.a. depth\).

```
 h      Balanced      Unbalanced, h = (n + 1)/2 - 1
 0:      ABCDE               ABCDE
        /     \             /     \
 1:    ABCD   E             ABCD   E
      /    \               /    \
 2:  AB    CD             ABC     D
    /  \  /  \           /   \
 3: A  B  C  D          AB   C
                       /  \
 4:                   A   B
```



