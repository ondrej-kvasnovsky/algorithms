# Design Linked List

Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes:`val` and`next`.`val`is the value of the current node, and`next` is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute`prev`to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

* get\(index\) : Get the value of the`index`-th node in the linked list. If the index is invalid, return`-1`
* addAtHead\(val\) : Add a node of value`val` before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
* addAtTail\(val\) : Append a node of value`val` to the last element of the linked list.
* addAtIndex\(index, val\) : Add a node of value`val` before the`index`-th node in the linked list. If`index` equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
* deleteAtIndex\(index\) : Delete the`index`-th node in the linked list, if the index is valid.

**Example:**

```
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1, 2);  // linked list becomes 1->2->3
linkedList.get(1);            // returns 2
linkedList.deleteAtIndex(1);  // now the linked list is 1->3
linkedList.get(1);            // returns 3
```

**Note:**

* All values will be in the range of`[1, 1000]`
* The number of operations will be in the range of `[1, 1000]`
* Please do not use the built-in LinkedList library.

## Solution

```
class MyLinkedList {

    Node head;
    
    public MyLinkedList() {
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    public int get(int index) {
        //System.out.println("get: " + index);
        int i = 0;
        Node current = head;
        while (i < index) {
            if (current != null) {
                current = current.next;
            } else  {
                return -1;
            }
            i++;
        }
        if (current == null) {
            return -1;
        }
        return current.value;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    public void addAtHead(int val) {
        //System.out.println("addAtHead: " + val);
        if (head == null) {
            head = new Node(val);
        } else {
            Node temp = head;
            head = new Node(val);
            head.next = temp;
        }
        //System.out.println(head);
    }
    
    /** Append a node of value val to the last element of the linked list. */
    public void addAtTail(int val) {
        //System.out.println("addAtTail: " + val);
        Node current = head;
        Node previous = null;
        while (current != null) {
            previous = current;
            current = current.next;
        }
        previous.next = new Node(val);
        //System.out.println(head);
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    public void addAtIndex(int index, int val) {
        //System.out.println("addAtIndex: " + index + " " + val);
        int i = 0;
        Node current = head;
        Node previous = head;
        while (i < index) {
            if (current != null) {
                previous = current;
                current = current.next;
            } else {
                return;
            }
            i++;
        }
        if (previous != null) {
            previous.next = new Node(val);
            previous.next.next = current;
        } else {
            head = new Node(val);
        }
       
        //System.out.println(head);
        return;
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    public void deleteAtIndex(int index) {
        //System.out.println("deleteAtIndex: " + index);
        int i = 0;
        // 1 -> 2 -> 3 (1)
        Node current = head;
        Node previous = null;
        Node next = null;
        while (i < index) {
            if (current != null) {
                previous = current;
                current = current.next;
                if (current != null) {
                    next = current.next;   
                }
            } else  {
                return;
            }
            i++;
        }
        if (previous != null && current != null) {
            previous.next = current.next;
        }
        //System.out.println(head);
    }
}
class Node {
    Node next;
    int value;
    public Node(int value) {
        this.value = value;
    }
    public String toString() {
        Node current = this;
        StringBuilder builder = new StringBuilder();
        while (current != null) {
            builder.append(current.value);
            builder.append(' ');
            current = current.next;
        }
        return builder.toString();
    }
}
/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```



