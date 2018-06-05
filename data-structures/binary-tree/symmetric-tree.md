# Symmetric Tree

Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

For example, this binary tree`[1,2,2,3,4,4,3]`is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following`[1,2,2,null,3,null,3]`is not:

```
    1
   / \
  2   2
   \   \
   3    3
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
    public boolean isSymmetric(TreeNode root) {
        // read two children and compare if they are the same (if not, stop and return false)
        // if yes, do the same left.right and right.left , then also for left.left and right.right
        if (root == null) { return true; }
        TreeNode left = root.left;
        TreeNode right = root.right;
        return isSym(left, right);
    }
    
    public boolean isSym(TreeNode left, TreeNode right) {
        if (left == null && right == null) return true;
        if (left == null || right == null) return false;
        boolean isSame = left.val == right.val;
        if (isSame) {
            boolean is = isSym(left.right, right.left) && isSym(left.left, right.right);
            return is;
        }
        return false;
    }
}
```



