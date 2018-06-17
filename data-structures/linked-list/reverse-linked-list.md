# Reverse Linked List

Let's start with a classic problem:

> Reverse a singly linked list.

One solution is to`iterate the nodes in original order and move them to the head of the list one by one`. It seems hard to understand. We will first use an example to go through our algorithm. 

### Algorithm Overview

---

Let's look at an example:

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/14/screen-shot-2018-04-14-at-163143.png)

Keep in mind that the black node 23 is our original head node.

1. First, we move the next node of the black node, which is node 6, to the head of the list:

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/14/screen-shot-2018-04-14-at-163336.png)

2. Then we move the next node of the black node, which is node 15, to the head of the list:

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/14/screen-shot-2018-04-14-at-163525.png)

3. The next node of the black node now is null. So we stop and return our new head node 15.

### More

---

In this algorithm, each node will be moved`exactly once`.

Therefore, the time complexity is`O(N)`, where N is the length of the linked list. We only use constant extra space so the space complexity is`O(1)`.

This problem is the foundation of many linked-list problems you might come across in your interview. If you are still stuck, our next article will talk more about the implementation details.

There are also many other solutions. You should be familiar with at least one solution and be able to implement it.

## Issue

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
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
    public ListNode reverseList(ListNode head) {
        // 1. using a stack
//         Stack<Integer> stack = new Stack<>();
//         ListNode node = head;
//         while (node != null) {
//             stack.add(node.val);
//             node = node.next;
//         }
        
//         if (stack.isEmpty()) {
//             return head;
//         }
        
//         ListNode newHead = new ListNode(stack.pop());
//         ListNode current = newHead;
//         while (!stack.isEmpty()) {
//             int val = stack.pop();
//             current.next = new ListNode(val);
//             current = current.next;
//         }
//         return newHead;
        
        // 2. flipping pointers from 1 -> 2 -> 3, to 1 <- 2 <- 3 (and return 3 at the end as new beggining)
        ListNode current = head;
        ListNode previous = null;
        while (current != null) {
            ListNode next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }
        return previous;
    }
}
```

Other solution. 

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
    public ListNode reverseList(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode currentHead = head;
        while (head.next != null) {
            ListNode p = head.next;
            head.next = p.next;
            p.next = currentHead;
            currentHead = p;
        }
        return currentHead;
    }
}
```



