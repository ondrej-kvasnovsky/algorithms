# Convert Sorted Array to Binary Search Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of_every_node never differ by more than 1.

**Example:**

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

## Solution

Start in the middle and add the other nodes recursively to left and right \(depending on what we read from the middle\).

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return createTree(nums, 0, nums.length - 1);
    }
    
    private TreeNode createTree(int[] nums, int left, int right) {
        if (left > right) return null;
        
        int mid = (left + right + 1) / 2;
        TreeNode node = new TreeNode(nums[mid]);
        
        node.left = createTree(nums, left, mid - 1);
        node.right = createTree(nums, mid + 1, right);
        
        return node;
    }
}
```



