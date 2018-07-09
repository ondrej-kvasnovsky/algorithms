# Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys **less than **the node's key.
* The right subtree of a node contains only nodes with keys **greater than **the node's key.
* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```
Input:
    2
   / \
  1   3
Output: true
```

**Example 2:**

```
    5
   / \
  1   4
     / \
    3   6
Output: false
Explanation: The input is: [5,1,4,null,null,3,6]. The root node's value
             is 5 but its right child's value is 4.
```

## Solution

Value on right must be smaller than its parent value. And value on right must be higher than its parent value. So we can make an algorithm that will check whether a value of left node is in range from min value to max value \(value of parent\). At the same time, a value on right must be higher than root value and less than max value. 

```
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean isValidBST(TreeNode root, long minVal, long maxVal) {
        if (root == null) return true;
        if (root.val >= maxVal || root.val <= minVal) return false;
        System.out.println("minVal: " + minVal + " maxVal: " + maxVal);
        return isValidBST(root.left, minVal, root.val) && isValidBST(root.right, root.val, maxVal);
    }
}
```

Here is a sample output of min and max values.

```
minVal: -9223372036854775808 maxVal: 9223372036854775807
minVal: -9223372036854775808 maxVal: 5
minVal: 5 maxVal: 9223372036854775807
```



