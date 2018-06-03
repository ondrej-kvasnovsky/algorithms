# Binary Tree Preorder Traversal

Given a binary tree, return the_preorder_traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        preorder(root, list);
        return list;
    }
    
    public void preorder(TreeNode node, List<Integer> list) {
        if (node == null) return;
        
        list.add(node.val);
        preorder(node.left, list);
        preorder(node.right, list);
    }
}
```



