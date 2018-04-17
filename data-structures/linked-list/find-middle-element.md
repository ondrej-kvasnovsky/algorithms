# Find Middle Element

If we want to find middle element of a linked list in one pass, we need to store middle element only when current index can be divided by 2.

Lets create a linked list that know its first and last element.

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

Then we create the linked list, put there few items and find the middle element.

```
public class Demo {
    public static void main(String... args) {
        LinkedList<String> list = new LinkedList<>();

        list.add(new Node<>("a"));
        list.add(new Node<>("b"));
        list.add(new Node<>("c"));
        list.add(new Node<>("d"));
        list.add(new Node<>("e"));
//        list.add(new Node<>("f"));
//        list.add(new Node<>("g"));
//        list.add(new Node<>("h"));
//        list.add(new Node<>("i"));
//        list.add(new Node<>("j"));
//        list.add(new Node<>("k"));

        Node<String> middle = findMiddle(list);

        System.out.println("Middle: " + middle.getValue());
    }

    private static Node<String> findMiddle(LinkedList<String> list) {
        int index = 0;

        Node<String> current = list.head();
        Node<String> middle = list.head();
        while (current.getNext() != null) {
            index += 1;
            if (index % 2 == 0) {
                middle = middle.getNext();
            }
            System.out.println(current.getNext().getValue());
            current = current.getNext();
        }
        if (index % 2 == 1) {
            middle = middle.getNext();
        }
        return middle;
    }
}
```



