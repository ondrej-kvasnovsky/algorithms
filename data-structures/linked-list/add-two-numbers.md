# Add Two Numbers

You are given two **non-empty **linked lists representing two non-negative integers. The digits are stored in **reverse order **and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode c1 = l1;
        ListNode c2 = l2;
        ListNode result = new ListNode(0);
        ListNode current = result;
        int remaining = 0;
        while(c1 != null || c2 != null) {
            int i1 = 0;
            if (c1 != null) i1 = c1.val;
            int i2 = 0;
            if (c2 != null) i2 = c2.val;
            int sum = i1 + i2 + remaining;
            if (sum >= 10) {
                remaining = 1;
                sum = sum - 10;
            } else {
                remaining = 0;
            }
            current.next = new ListNode(sum);
            current = current.next;
            
            if (c1 != null) c1 = c1.next;
            if (c2 != null) c2 = c2.next;
        }
        if (remaining == 1) {
            current.next = new ListNode(remaining);
        }
        return result.next;
    }
}
```



