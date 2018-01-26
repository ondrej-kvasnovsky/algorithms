# Recursion

Lets create a simple method that will use recursion to calculate sum of all numbers contained in an array.

> We won't be able to get sum of large arrays with many items because of limitations of Java.

```
class Recursion {

    public static void main(String[] args) {
        Recursion recursion = new Recursion();

        int sum1 = recursion.sum(new int[]{1}, 0);
        System.out.println(sum1);

        int sum2 = recursion.sum(new int[]{1, 2, 3}, 0);
        System.out.println(sum2);
    }

    int sum(int[] array, int index) {
        if (index >= array.length) return 0;
        int value = array[index];
        return value + sum(array, ++index);
    }
}
```

### Iterate from root to leaves

Lets create tree structure and then recursively iterate through it and print the tree with intendation. 

```
class NodeRecursion {

    public static void main(String[] args) {
        Node root = new Node("Root");
        Node first = new Node("First");
        first.children.add(new Node("Under First"));
        root.children.add(first);
        root.children.add(new Node("Second"));
        Node third = new Node("Third");
        third.children.add(new Node("Under Third"));
        root.children.add(third);

        NodeRecursion r = new NodeRecursion();
        r.print(root, 0);
    }

    public void print(Node node, int spaces) {
        if (node == null) return;
        if (!node.children.isEmpty()) {
            node.children.forEach(it -> print(it, spaces + 1));
        }
        String emptySpaces = createEmptySpaces(spaces);
        System.out.println(emptySpaces + node.value);
    }

    private String createEmptySpaces(int spaces) {
        String emptySpaces = "";
        for (int i = 0; i < spaces; i++) {
            emptySpaces += " ";
        }
        return emptySpaces;
    }
}

class Node {
    String value;
    List<Node> children = new ArrayList<>();

    Node(String value) {
        this.value = value;
    }
}
```

Here is the output. 

```
Root
 First
  Under First
 Second
 Third
  Under Third
```

### Iterate from leaves to root

It is enough just to move two lines of code from previous example down to iterate the tree structure from leave to root. 

```
void print(Node node, int spaces) {
  if (node == null) return;
  if (!node.children.isEmpty()) {
    node.children.forEach(it -> print(it, spaces + 1));
  }
  String emptySpaces = createEmptySpaces(spaces);
  System.out.println(emptySpaces + node.value);
}
```

Here is the output. 

```
  Under First
 First
 Second
  Under Third
 Third
Root
```

### Binary tree traversal

Example. 

```
class BinaryTreeRecursion {

    public static void main(String[] args) {
        BinaryNode root = new BinaryNode("Root");
        BinaryNode first = new BinaryNode("Under Root Right");
        root.right = first;
        root.left = new BinaryNode("Under Root Left");
        first.right = new BinaryNode("Under First Right");
        BinaryNode third = new BinaryNode("Third");
        first.left = third;
        third.left = new BinaryNode("Under Third");

        BinaryTreeRecursion r = new BinaryTreeRecursion();
        r.print(root, 0);
        r.printIterative(root, 0);
    }

    private void print(BinaryNode node, int spaces) {
        if (node == null) return;
        String emptySpaces = createEmptySpaces(spaces);
        System.out.println(emptySpaces + node.value);
        if (node.left != null) {
            print(node.left, spaces + 1);
        }
        if (node.right != null) {
            print(node.right, spaces + 1);
        }
    }

    private void printIterative(BinaryNode node, int spaces) {
        if (node == null) return;
        Stack<BinaryNode> stack = new Stack<>();
        stack.push(node);
        while (!stack.isEmpty()) {
            BinaryNode fromStack = stack.pop();
            String emptySpaces = createEmptySpaces(fromStack.spaces);
            System.out.println(emptySpaces + fromStack.value);
            if (fromStack.left != null) {
                fromStack.left.spaces = fromStack.spaces + 1;
                stack.push(fromStack.left);
            }
            if (fromStack.right != null) {
                fromStack.right.spaces = fromStack.spaces + 1;
                stack.push(fromStack.right);
            }
        }
    }

    private String createEmptySpaces(int spaces) {
        String emptySpaces = "";
        for (int i = 0; i < spaces; i++) {
            emptySpaces += " ";
        }
        return emptySpaces;
    }
}

class BinaryNode {
    String value;
    BinaryNode left;
    BinaryNode right;
    int spaces;

    public BinaryNode(String value) {
        this.value = value;
    }
}
```



