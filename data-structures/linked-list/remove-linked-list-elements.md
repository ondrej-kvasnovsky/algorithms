# Remove Linked List Elements

Remove all elements from a linked list of integers that have value**val**.

**Example:**

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

## Solution

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode current = head;
        ListNode previous = null; 
        // 1 -> 2 (1)
        // 1 -> 2 (2)
        // 1 -> 1 (1)
        // 1 (1)
        // 1, 2, 2, 1
        while (current != null) {
            int value = current.val;
            if (val == value) {
                if (previous != null) {
                    previous.next = current.next;
                    current = previous.next;
                } else {
                    head = current.next;
                    current = head;
                    if (current == null) {
                        break;
                    }
                    continue;
                }
            } else {
                previous = current;
                current = current.next;
            }
        }
        return head;
    }
}
```

Another solution. 

```
public ListNode removeElements(ListNode head, int val) {
    if (head == null) return null;
    ListNode pointer = head;
    while (pointer.next != null) {
        if (pointer.next.val == val) {
            pointer.next = pointer.next.next;
        } else {
            pointer = pointer.next;
        }
    }
    return head.val == val ? head.next : head;
}
```

Recursive solution. 

```
public ListNode removeElements(ListNode head, int val) {
    if (head == null) return null;
    head.next = removeElements(head.next, val);
    return head.val == val ? head.next : head;
}
```



