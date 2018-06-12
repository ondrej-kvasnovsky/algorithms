# Search in a Binary Search Tree

Given the root node of a binary search tree \(BST\) and a value. You need to find the node in the BST that the node's value equals the given value. Return the subtree rooted with that node. If such node doesn't exist, you should return NULL.

For example, 

```
Given the tree:
        4
       / \
      2   7
     / \
    1   3

And the value to search: 2
```

You should return this subtree:

```
      2     
     / \   
    1   3
```

In the example above, if we want to search the value`5`, since there is no node with value`5`, we should return`NULL`.  


## Solution

Get the value of a node and compare it with value we want to find. If value is less or equal then go to left if value is greater go right. And repeat this for all the nodes. 

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
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) return null;
        TreeNode current = root;
        while (current != null) {
            if (current.val == val) {
                return current;
            }
            if (val < current.val) {
                current = current.left;
            } else {
                current = current.right;
            }            
        }
        return null;
    }
}
```



