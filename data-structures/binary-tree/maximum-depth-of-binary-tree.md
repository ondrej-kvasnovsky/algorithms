# Maximum Depth of Binary Tree

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

## Solution

I don't know why I made this solution, I just found it some time ago. And I don't like anymore. There is another solution for the same problem below. 

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
    int max = 0;
    
    // 1 -> 1
    // 1 -> 2->3,4
    public int maxDepth(TreeNode root) {
        // counter = 0
        // recursively come to end of each node and count all nodes, 
        //   then change max only if depth is bigger & .left or .right is null
        iterate(root, 0);
        
        return max;
    }
    
    public void iterate(TreeNode node, int count) {
        if (node == null) {
            max = Math.max(max, count);
            return;
        }
        count++;
        iterate(node.left, count);
        iterate(node.right, count);
    }
}
```

The other, more nice solution. 

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

    public int maxDepth(TreeNode root) {
        return depth(root, 0);
    }
    
    private int depth(TreeNode node, int depth) {
        if (node == null) {
            return depth;
        }
        
        int leftMax = depth(node.left, depth + 1);
        int rightMax = depth(node.right, depth + 1);
        return Math.max(leftMax, rightMax);
    }
}
```



