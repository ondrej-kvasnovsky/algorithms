# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

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



