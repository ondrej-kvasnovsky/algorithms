# Count Univalue Subtrees

Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

**Example :**

```
Input:  root = [5,1,5,5,5,null,5]

              5
             / \
            1   5
           / \   \
          5   5   5

Output: 4
```

## Solution

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
    int counter = 0;
    public int countUnivalSubtrees(TreeNode root) {
        traverse(root, 0);
        return counter;
    }
    
    private boolean traverse(TreeNode node, int parentValue) {
        if (node == null) {
            return true;
        }
        
        int val = node.val;
        boolean left = traverse(node.left, val);
        boolean right = traverse(node.right, val);
        if (left && right) {
            counter++;
        }
        
        return left && right && parentValue == val;
    }
}
```



