# Linked List

The basic element of linked list is the link. 

```
class Link<T> {

    T value
    Link<T> next
}
```

Then we can compose these links in main class that will represent the linked list. 

```
class LinkedList<T> {

    Link<T> first
    int size

    void add(T value) {
        Link<T> link = new Link<>(value: value)
        if (first) {
            Link<T> temp = first
            while (temp.next) {
                temp = temp.next
            }
            temp.next = link
        } else {
            first = link
        }
        size++
    }

    int size() {
        size
    }

    T find(T value) {
        Link<T> temp = first 
        while (temp.next) { // until temp.next is not null
            if (temp.value == value) {
                return temp.value
            }
            temp = temp.next
        }
        return null
    }

    void insert(int index, T value) {
        Link<T> temp = first
        int i = 0
        while (temp.next) {
            if (index - 1 == i) {
                Link<T> moving = temp.next
                temp.next = new Link<T>(value: value)
                temp.next.next = moving
                size++
                break
            }
            temp = temp.next
            i++
        }
    }
}
```



