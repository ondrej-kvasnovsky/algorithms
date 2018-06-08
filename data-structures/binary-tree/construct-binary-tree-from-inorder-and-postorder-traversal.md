# Construct Binary Tree from Inorder and Postorder Traversal

Given inorder and postorder traversal of a tree, construct the binary tree.

**Note:**  
You may assume that duplicates do not exist in the tree.

For example, given

```
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

Explanation:

**The Basics:**

Inorder, postorder, and preorder are all flavors of Depth First Search. The difference between them is when the child nodes are visited relative to the root node.

Inorder is left, root, right  
Postorder is left, right, root  
Preorder is root, left, right

_Note: outside of the context of this question, the order of the child nodes can be reversed. The thing that matters is when the root node is visited relative to the child nodes._

**Observation 1:**

If we reverse the postorder array, we end up with a preorder array \(only root, right, left instead of root, left, right\).

**Observation 2:**

The relative positions of the values in the inorder array can tell us whether a value appears on the left or right side of another value in the tree.

**Strategy:**

Reverse the postorder traversal to get a preorder traversal. If a value in the preorder traversal is on the right side of its previous value, the current value is the previous value's right child \(because the preorder goes root, right, left and so the right node shows up immediately after the root and it keeps diving right\). Otherwise, the current value might be the previous value's left child, but it might also be the left child of a grandparent or great-grandparent, and so we need to check up the tree until we either reach the root or reach a node that is still on the left of the current value.

**Pseudo code:**

```
save the indices of the values in the inorder array in a map so we can know the relative positon of values in the tree

starting from the end of the postorder array, create a node for the root

push the root node on to a stack

for (the remaining numbers in the postorder array, going in reverse order)
{
    create a node for the current number
    if the current number is on the right side of the node at the top of the stack
    {
        set the newly created node to be the node at the top of the stack's right child
    }
    else
    {
        while (the stack is not empty AND the number is on the left of the node at the top of the stack)
        {
            set the parent to be the result of popping the stack
        }
        set the newly created node to be the parent's left child
    }
    push the newly created node on to the stack
}

return the root node
```

**Code:**

```
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder.length == 0) {
            return null;
        }
        
        Map<Integer, Integer> order = new HashMap<>();
        for (int i = 0; i < inorder.length; i ++) {
            order.put(inorder[i], i);
        }
        
        TreeNode root = new TreeNode(postorder[postorder.length - 1]);
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        for (int i = postorder.length - 2; i >= 0; i --) {
            TreeNode curr = new TreeNode(postorder[i]);
            if (order.get(curr.val) > order.get(stack.peek().val)) {
                stack.peek().right = curr;
            } else {
                TreeNode parent = stack.pop();
                while (!stack.isEmpty() && (order.get(curr.val) < order.get(stack.peek().val))) {
                    parent = stack.pop();
                }
                parent.left = curr;
            }
            stack.push(curr);
        }
        
        return root;
    }
}
```

## Solution

```
    3
   / \
  9  20
    /  \
   15   7
```

What we get from those two fields \(different order of elements\).

```
inorder = [9,3,15,20,7] left to 3 is 9, 15 is left to 20 and 7 is right to 20 - we can use this to
find whether an element is on left or right side (while building a tree)
```

```
postorder = [9,15,7,20,3] if we go from end, we can reconstruct tree
```

Here is a solution. 

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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder.length == 0 || postorder.length == 0) return null;
        Map<Integer, Integer> mapping = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            mapping.put(inorder[i], i);
        }
        TreeNode root = new TreeNode(postorder[postorder.length - 1]);
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        for (int i = postorder.length - 2; i >= 0; i--) {
            int val = postorder[i];
            TreeNode current = new TreeNode(val);
            int stackVal = stack.peek().val;
            if (mapping.get(val) > mapping.get(stackVal)) {
                stack.peek().right = current;
            } else {
                TreeNode parent = stack.pop();
                while (!stack.isEmpty() && mapping.get(val) < mapping.get(stack.peek().val)) { 
                    parent = stack.pop();
                }
                parent.left = current;
            }
            stack.push(current);
        }
        return root;
    }
}
```



