# Inorder Successor in BST

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

**Note**: If the given node has no in-order successor in the tree, return`null`.

**Example 1:**

```
Input: root = [2,1,3], p = 1

  2
 / \
1   3

Output: 2
```

**Example 2:**

```
Input: root = [5,3,6,2,4,null,null,1], p = 6

      5
     / \
    3   6
   / \
  2   4
 /   
1

Output: null
```

## Solution

Recursive solution.

```
class Solution {
    TreeNode ceiling = null;
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null || p == null) {
            return ceiling;
        }
        if (root.val <= p.val) {
            inorderSuccessor(root.right, p);
        } else {
            ceiling = root;
            inorderSuccessor(root.left, p);
        }
        return ceiling;
    }
}
```

Another iterative solution. 

```
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    TreeNode succ = null;
    while (root != null) {
        if (p.val < root.val) {
            succ = root;
            root = root.left;
        } else {
            root = root.right;
        }
    }
    return succ;
}
```





