# Closest Binary Search Tree Value

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

* Given target value is a floating point.
* You are guaranteed to have only one unique value in the BST that is closest to the target.

**Example:**

```
Input: root = [4,2,5,1,3], target = 3.714286

    4
   / \
  2   5
 / \
1   3

Output: 4
```

## Solution

In this solution, we iterate through the nodes and find minimum difference between node value and target value.

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
    public int closestValue(TreeNode root, double target) {
        // iterate through the nodes and find minimum difference between node value and target value
        // 4 - 3.7 -> 0.3 (correct answer)
        // 2 - 3.7 -> 1.7
        // 1 - 3.7 -> 2.7
        // 3 - 3.7 -> 0.7
        // 5 - 3.7 -> 1.3
        if (root == null) return -1;
        traverse(root, target);
        return minNode.val;
    }
    
    double minVal = Double.MAX_VALUE;
    TreeNode minNode;
    
    private void traverse(TreeNode node, double target) {
        if (node == null) return;
        double difference = Math.abs(node.val - target);
        if (difference < minVal) {
            minVal = difference;
            minNode = node;
        }
        traverse(node.left, target);
        traverse(node.right, target);
    }
}
```

Other solution following the same principle, but without recursion. 

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
    public int closestValue(final TreeNode root, final  double target) {
        TreeNode current = root;
        int ret = current.val;   
        while (current != null){
            if (Math.abs(target - current.val) < Math.abs(target - ret)){
                ret = current.val;
            }
            if (current.val > target) {
                current = current.left;
            } else {
                current = current.right;
            }
            
        }     
        return ret;
    }
}
```



