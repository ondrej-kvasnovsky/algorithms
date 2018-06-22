# Rotate List

Given a linked list, rotate the list to the right by_k_places, where_k_is non-negative.

**Example 1:**

```
Input: 1->2->3->4->5->NULL, k = 2
Output: 4->5->1->2->3->NULL
Explanation:
rotate 1 steps to the right: 5->1->2->3->4->NULL
rotate 2 steps to the right: 4->5->1->2->3->NULL
```

**Example 2:**

```
Input: 0->1->2->NULL, k = 4
Output: 2->0->1->NULL
Explanation:
rotate 1 steps to the right: 2->0->1->NULL
rotate 2 steps to the right: 1->2->0->NULL
rotate 3 steps to the right: 0->1->2->NULL
rotate 4 steps to the right: 2->0->1->NULL
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
    public ListNode rotateRight(ListNode head, int k) {
        ListNode fake = new ListNode(-1);
        ListNode slow = fake;
        ListNode fast = fake;
        fake.next = head;
        
        int len = 0;
        while (fast.next != null) {   // fast REACH tail && Count len
            fast = fast.next; len++;
        }
        if (len == 0) return null;   // CHECK null
        
        k %= len;
        for (int i=0; i<len-k; i++)  // slow REACH before the rotated point 
            slow = slow.next;
        
        fast.next = fake.next;      // CONNECT
        fake.next = slow.next;
        slow.next = null;
        
        return fake.next; 
    }
}
```



