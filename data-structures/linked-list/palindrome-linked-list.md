# Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

**Example 1:**

```
Input: 1->2
Output: false
```

**Example 2:**

```
Input: 1->2->2->1
Output: true
```

**Follow up:**  
Could you do it in O\(n\) time and O\(1\) space?

## Solution

Using stack.

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
    public boolean isPalindrome(ListNode head) {
        // read all items with two pointers (slow, fast * 2, when fast.next is null, slow is in the middle), put all middle into stack and then continue reading the slow and all values must match values from stack, if not, return false
        if (head == null || head.next == null) return true;
        ListNode slow = head;
        ListNode fast = head;
        Stack<ListNode> stack = new Stack<>();
        while (fast != null && fast.next != null) {
            stack.add(slow);
            slow = slow.next;
            fast = fast.next.next;
        }

        if (fast != null) { // if fast is not null, the number of elements is odd, 
        // and we want to move slow by one, e.g. 1 -> 0 -> 1
            slow = slow.next;
        }

        while (slow != null) {
            if (stack.isEmpty()) return false;
            ListNode fromStack = stack.pop();
            if (slow.val != fromStack.val) {
                return false;
            }
            slow = slow.next;
        }
        return true;
    }
}
```

Other solutions. 

```
private static boolean isPallindrome(Node head){
    if (head == null) {
        return true;
    }
	
    Node temp = head;
    Node prev = new Node(head.data);
	
    while (temp.next != null){
        Node curr = new Node(temp.next.data);
        curr.next = prev;
        prev = curr;
        temp = temp.next;
    }
	
    Node ptr1 = head;
    Node ptr2 = prev;
	
    while (ptr1 != null) {
        if (ptr1.data != ptr2.data) {
            return false;
        }	
        ptr1 = ptr1.next;
        ptr2 = ptr2.next;
    }
    return true;
}
```

Space optimized. 

```
private static boolean isPallindromeSpaceOptimzed(Node head){
    if(head == null || head.next == null) {
        return true;
    }

    Node fast = head;
    Node slow = head;
    
    while (fast.next != null && fast.next.next != null) {
        fast = fast.next.next;
        slow = slow.next;
    }
    
    Node head2 = slow.next;
    slow.next = null;
    
    //reverse the second half of the list
    Node ptr1 = head2;
    Node ptr2 = ptr1.next;
    
    while (ptr1.next != null && ptr2.next != null) {
        Node temp = ptr2.next;
        ptr2.next = ptr1;
        ptr1 = ptr2;
        ptr2 = temp;
    }
    
    head2.next = null;
    
    // comparing the two sub lists
    Node p1 = (ptr2 == null ? ptr1 : ptr2);
    Node p2 = head;
    
    while (p1 != null) {
        if(p1.data != p2.data) {
            return false;
        }        
        p1 = p1.next;
        p2 = p2.next;
    }
    
    return true;
}
```



