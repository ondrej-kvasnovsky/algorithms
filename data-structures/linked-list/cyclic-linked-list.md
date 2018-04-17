# Cyclic Linked List

How to find whether the linked list is cyclic, so there is a loop in it? There is a cycle in a linked list when an element is referred by two other elements. In other words, two elements are referring to the same element.

```
if (element == element1 || element == element2) { 
  // there is a loop!
}
```

We want to iterate through the array using three pointers. The first pointer is going from one node to another, on by one. The other to pointers will be faster. If one of the faster pointers catches the slow pointer, there is a loop.

Lets create the following loop in a linked list.

```
a -> b -> c -> d -> e -> a
```

Lets iterate the list using slow pointer and two fast pointers. Each line means one iteration.

```
1. slow: a, fast1: b, fast2: c
2. slow: b, fast1: d, fast2: e
3. slow: c, fast1: a, fast2: b
4. slow: d, fast1: c, fast2: d (d == d, so there is a loop, otherwise, it would never get there)
```

Here is the algorithm.

```
public class Demo {

    public static void main(String... args) {
        LinkedList<String> list = new LinkedList<>();

        Node<String> a = new Node<>("a");
        list.add(a);
        Node<String> b = new Node<>("b");
        list.add(b);
        Node<String> c = new Node<>("c");
        list.add(c);
        Node<String> d = new Node<>("d");
        list.add(d);
        Node<String> e = new Node<>("e");
        list.add(e);

        // add a loop
        e.setNext(a);

        // find a loop -> two nodes are referencing the same node
        // Simultaneously go through the list by ones (slow iterator) and by twos (fast iterator).
        // If there is a loop the fast iterator will go around that loop twice as fast as the slow iterator.
        // The fast iterator will lap the slow iterator within a single pass through the cycle.
        // Detecting a loop is then just detecting that the slow iterator has been lapped by the fast iterator.

        Node<String> startingNode = list.head().getNext();
        Node<String> slowPointer = startingNode;
        Node<String> fastPointer1;
        Node<String> fastPointer2 = startingNode;

        // no loop
        // a -> b -> c -> d
        // a | b
        // b | d
        // c | null -> ends the while loop
        // a -> b -> c -> -> d -> e -> a
        // ------------->
        while (slowPointer.getNext() != null                          // a | b | c | d
                && (fastPointer1 = fastPointer2.getNext()) != null    // b | d | a | c
                && (fastPointer2 = fastPointer1.getNext()) != null) { // c | e | b | d
            System.out.println("combination: " + slowPointer.getValue() + ", " + fastPointer1.getValue() + ", " + fastPointer2.getValue());
            if (slowPointer == fastPointer1 || slowPointer == fastPointer2) {
                System.out.println("Loop identified!");
                break;
            }
            slowPointer = slowPointer.getNext();
        }
    }
}
```

We are going to use this implementation of a linked list.

```
class LinkedList<T> {
    private Node<T> head;
    private Node<T> tail;

    public LinkedList() {
        head = new Node<>(null);
        tail = head;
    }

    public Node<T> head() {
        return head;
    }

    public void add(Node<T> node) {
        tail.setNext(node);
        tail = node;
    }
}

class Node<T> {
    private Node<T> next;
    private T value;

    public Node(T value) {
        this.value = value;
    }

    public Node<T> getNext() {
        return next;
    }

    public void setNext(Node<T> next) {
        this.next = next;
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return value.toString();
    }
}
```



