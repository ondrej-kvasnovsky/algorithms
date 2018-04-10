# Binary Search Tree

[Binary Search Tree](https://en.wikipedia.org/wiki/Binary_search_tree) is a data structure to store hierarchical data where each node has only two leaf nodes and nodes are sorted from left to right. BST is also called ordered or sorted binary tree.

BST is good for searching in general `O(log n)`. Heaps are the best when we want to get maximum or minimum of set of values, complexity of `O(1)`. More about the difference between [heap and BST](https://cs.stackexchange.com/questions/27860/whats-the-difference-between-a-binary-search-tree-and-a-binary-heap).

The basic algorithm is: when we want to put a value into the tree, we go from the root and we put smaller values on left and higher values on right side.

```
import java.util.LinkedList;
import java.util.Queue;

class BinarySearchTree<T extends Comparable<T>> {

    TreeNode<T> root;

    public void add(T value) {
        if (root == null) {
            root = new TreeNode<>(value);
        } else {
            addNode(value, root);
        }
    }

    public void addNode(T value, TreeNode<T> node) {
        if (isValueHigherThanNodeValue(value, node)) {
            // higher values go on left
            addToRight(value, node);
        } else {
            // lower values go on left
            addToLeft(value, node);
        }
    }

    private void addToLeft(T value, TreeNode<T> node) {
        if (node.left == null) {
            node.left = new TreeNode<>(value);
            return;
        }
        addNode(value, node.left);
    }

    private void addToRight(T value, TreeNode<T> node) {
        if (node.right == null) {
            node.right = new TreeNode<>(value);
            return;
        }
        addNode(value, node.right);
    }

    private boolean isValueHigherThanNodeValue(T value, TreeNode<T> current) {
        return value.compareTo(current.value) > 0;
    }

    public String toString() {
        return asString(root, 0);
    }

    private String asString(TreeNode<T> node, int level) {
        if (node == null) return null;
        String result = spaces(level) + node.value.toString() + " \n";
        level++;
        if (node.left != null) {
            result += asString(node.left, level);
        }
        if (node.right != null) {
            result += asString(node.right, level);
        }
        return result;
    }

    private String spaces(int level) {
        String spaces = "";
        for (int i = 0; i < level; i++) {
            spaces += "-";
        }
        return spaces;
    }

    // read to queue in 'breath first' order
    public Queue<TreeNode<T>> readToQueue(TreeNode<T> node) {
        Queue<TreeNode<T>> queue = new LinkedList<>();
        Queue<TreeNode<T>> temp = new LinkedList<>();
        temp.add(node);
        while (temp.size() > 0) {
            TreeNode<T> n = temp.poll();
            queue.add(n);
            if (n.left != null) {
                temp.add(n.left);
            }
            if (n.right != null) {
                temp.add(n.right);
            }
        }
        return queue;
    }

    // breath first or a.k.a. level order traversal
    // -> A
    // -> B -> C
    // -> D -> E -> F -> G
    public String breathFirst(TreeNode<T> node) {
        Queue<TreeNode<T>> queue = new LinkedList<>();
        queue.add(node);
        String value = "";
        while (queue.size() > 0) {
            TreeNode<T> n = queue.poll();
            value += n.value.toString() + " ";
            if (n.left != null) {
                queue.add(n.left);
            }
            if (n.right != null) {
                queue.add(n.right);
            }
        }
        return value;
    }

    enum Order {
        Pre, In, Post
    }

    // pre order traversal - root, left, right
    // in order traversal - left, root, right
    // post order traversal - left, right root
    public String depthFirst(TreeNode<T> node, Order order) {
        if (node == null) return null;
        String value = "";
        if (order.equals(Order.Pre)) {
            value += node.value.toString() + " ";
        }
        if (node.left != null) {
            value += depthFirst(node.left, order);
        }
        if (order.equals(Order.In)) {
            value += node.value.toString() + " ";
        }
        if (node.right != null) {
            value += depthFirst(node.right, order);
        }
        if (order.equals(Order.Post)) {
            value += node.value.toString() + " ";
        }

        return value;
    }
}
```

We have implemented few types of tree traversal. Here is code that creates BST and uses couple of BST traversals.

```
import java.util.LinkedList;
import java.util.Queue;

public class BinarySearchTreeDemo {
    public static void main(String... args) {
        BinarySearchTree<Integer> bst = new BinarySearchTree<>();

        bst.add(10);
        bst.add(5);
        bst.add(15);
        bst.add(2);
        bst.add(0);
        bst.add(25);
        bst.add(20);

        System.out.println("BST:");
        System.out.println(bst);

        System.out.println("Breath First:");
        System.out.println(bst.breathFirst(bst.root));

        System.out.println("Pre order:");
        String preOrder = bst.depthFirst(bst.root, BinarySearchTree.Order.Pre);
        System.out.println(preOrder);

        System.out.println("In order:");
        String inOrder = bst.depthFirst(bst.root, BinarySearchTree.Order.In);
        System.out.println(inOrder);

        System.out.println("Post order:");
        String postOrder = bst.depthFirst(bst.root, BinarySearchTree.Order.Post);
        System.out.println(postOrder);
    }
}
```

Here is the output.

```
BST:
10 
-5 
--2 
---0 
-15 
--25 
---20 

Breath First:
10 5 15 2 25 0 20 
Pre order:
10 5 2 0 15 25 20 
In order:
0 2 5 10 15 20 25 
Post order:
0 2 5 20 25 15 10
```



