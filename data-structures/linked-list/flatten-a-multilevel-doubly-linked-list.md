# Flatten a Multilevel Doubly Linked List

You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.

**Example:**

```
Input:
 1---2---3---4---5---6--NULL
         |
         7---8---9---10--NULL
             |
             11--12--NULL

Output:
1-2-3-7-8-11-12-9-10-4-5-6-NULL
```

**Explanation for the above example:**

Given the following multilevel doubly linked list:

![](https://leetcode.com/static/images/problemset/MultilevelLinkedList.png)

We should return the following flattened doubly linked list:

![](https://leetcode.com/static/images/problemset/MultilevelLinkedListFlattened.png)

## Solution

Solution is inspired by this article [here](https://mikkqu.com/flatten-a-multilevel-doubly-linked-list/). The idea is to change pointers so it "inserts" child into parent and parent.next.![](/assets/import.png)

```
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;

    public Node() {}

    public Node(int _val,Node _prev,Node _next,Node _child) {
        val = _val;
        prev = _prev;
        next = _next;
        child = _child;
    }
};
*/
class Solution {
    public Node flatten(Node head) {
        Node parent = head;
        while (parent != null) {
            Node child = parent.child;
            if (child != null) {
                Node lastChild = child;
                while (lastChild.next != null) { // find last child
                    lastChild = lastChild.next;
                }
                if (parent.next != null) { // if parent has next, set child as previous of the next one
                    // if parent.next is null, it can't reference back
                    parent.next.prev = lastChild;
                }
                // make links (insert child into parent)
                parent.child.prev = parent; 
                lastChild.next = parent.next;
                parent.next = parent.child;
                parent.child = null;
            }
            parent = parent.next;
        }
        return head;
    }
}
```



