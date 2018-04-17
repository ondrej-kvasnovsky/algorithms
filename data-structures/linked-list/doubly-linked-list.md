# Doubly Linked List

Doubly linked list knows its next and also its previous item.

```
public class Demo {
    public static void main(String... args) {
        DoublyLinkedList<Integer> list = new DoublyLinkedList<>();
        list.add(new DoubleNode<>(1));
        list.add(new DoubleNode<>(2));
        list.add(new DoubleNode<>(3));
    }
}

class DoublyLinkedList<T> {
    private DoublyNode<T> head = new DoublyNode<>(null);
    private DoublyNode<T> tail;

    public DoublyLinkedList() {
        tail = head;
    }

    public void add(DoubleNode<T> item) {
        tail.setNext(item);
        tail = item;
    }
}

class DoublyNode<T> {
    private DoublyNode<T> next;
    private DoublyNode<T> previous;
    private T value;

    public DoublyNode(T value) {
        this.value = value;
    }

    public DoublyNode<T> getNext() {
        return next;
    }

    public void setNext(DoublyNode<T> next) {
        this.next = next;
    }

    public DoublyNode<T> getPrevious() {
        return previous;
    }

    public void setPrevious(DoublyNode<T> previous) {
        this.previous = previous;
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }
}
```



