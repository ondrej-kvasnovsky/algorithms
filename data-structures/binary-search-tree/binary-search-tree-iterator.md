# Binary Search Tree Iterator

Implement an iterator over a binary search tree \(BST\). Your iterator will be initialized with the root node of a BST.

Calling `next()`will return the next smallest number in the BST.

**Note:**`next()`and`hasNext()`should run in average O\(1\) time and uses O\(h\) memory, wherehis the height of the tree.

## Solution

Put all left values into stack. Then when getting a next one, pop a node from stack and add the right into stack together with its all left nodes. That will make sure the values are sorted. 

```
public class BSTIterator {
    private final Stack<TreeNode> stack;
    
    public BSTIterator(TreeNode root) {
        stack = new Stack<>();
        TreeNode cur = root;
        while (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode node = stack.pop();
        
        // Traversal cur node's right branch
        TreeNode cur = node.right;
        while (cur != null){
            stack.push(cur);
            cur = cur.left;
        }
        
        return node.val;
    }
}
```



