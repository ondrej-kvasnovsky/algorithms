# Binary Tree Postorder Traversal

Given a binary tree, return the_postorder_traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        traverse(root, list);
        return list;
    }
    private void traverse(TreeNode node, List<Integer> list) {
        if (node == null) return;
        traverse(node.left, list);
        traverse(node.right, list);
        list.add(node.val);
    }
}
```



