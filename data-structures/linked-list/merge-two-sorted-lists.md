# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution

Here is a solution.

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // read l1
        // read l2
        // if l1 is less or equal than l2 (1 <= 5, 1 <= 1) => write l1 value and continue with l1
        // else write l2 value, read another l2 value
        // repeat until value of l1 or value of l2 is null
        ListNode result = new ListNode(0);
        ListNode current = result;

        ListNode list1 = l1;
        ListNode list2 = l2;

        while (list1 != null || list2 != null) {
            if (list1 != null && list2 != null) {
                int v1 = list1.val;
                int v2 = list2.val;
                if (v1 <= v2) {
                    ListNode n = new ListNode(v1);
                    current.next = n;
                    current = n;
                    list1 = list1.next;
                } else {
                    ListNode n = new ListNode(v2);
                    current.next = n;
                    current = n;
                    list2 = list2.next;
                }
            } else if (list1 != null) {
                int v1 = list1.val;
                ListNode n = new ListNode(v1);
                current.next = n;
                current = n;
                list1 = list1.next;
            } else if (list2 != null) {
                int v2 = list2.val;
                ListNode n = new ListNode(v2);
                current.next = n;
                current = n;
                list2 = list2.next;
            }
        }

        return result.next;
    }
}
```

Solution using recursion. 

```
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        } else if (l2 == null) {
            return l1;
        } else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

Other iterative approach. 

```
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // maintain an unchanging reference to node ahead of the return node.
        ListNode prehead = new ListNode(-1);

        ListNode prev = prehead;
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                prev.next = l1;
                l1 = l1.next;
            } else {
                prev.next = l2;
                l2 = l2.next;
            }
            prev = prev.next;
        }

        // exactly one of l1 and l2 can be non-null at this point, so connect
        // the non-null list to the end of the merged list.
        prev.next = l1 == null ? l2 : l1;

        return prehead.next;
    }
}
```



