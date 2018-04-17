# Find Nth Element from End

We want to find Nth element from the end in a linked list in one pass. 

Lets create counter that will count what element we are reading. Then we create to pointers. The first pointer will be normal pointer that iterates through all the elements in the array. The second pointer will be a slow pointer and will be set after we have read N elements from the linked list. After the index is higher than N, we can update the slow pointer every iterations. 

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
        Node<String> f = new Node<>("f");
        list.add(f);

        // index
        // 2    -> 3    -> 4 -> 5 -> 6
        // 1. fast
        // b    -> c    -> d -> e -> f
        // 2. slow
        // null -> null -> a -> b -> d

        int index = 1;
        Node<String> fast = a;
        Node<String> slow = null;
        while (fast.getNext() != null) {
            index++;
            fast = fast.getNext();
            if (index > 3) { //  slow it down by 3
                if (slow == null) {
                    slow = a.getNext();
                } else {
                    slow = slow.getNext(); // if index is bigger than 3, move slow every iteration
                }
            }
            System.out.println(fast.getValue() + ", " + slow + " - " + index);
        }

        System.out.println("Third: " + slow.getValue());
    }
}
```



