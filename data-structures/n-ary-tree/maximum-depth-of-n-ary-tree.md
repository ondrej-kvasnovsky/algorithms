# Maximum Depth of N-ary Tree

Given a n-ary tree, find its maximum depth. The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node. For example, given a`3-ary`tree:

![](https://leetcode.com/static/images/problemset/NaryTreeExample.png)

We should return its max depth, which is 3.

## Solution

```
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
    int max = Integer.MIN_VALUE;
    
    public int maxDepth(Node root) {
        // need to find depth of all children
        if (root == null) return 0;
        return depth(root, 1);
    }
    
    private int depth(Node node, int depth) {
        if (node == null) {
            return depth;
        }
        int newDepth = depth + 1;
        List<Node> children = node.children;
        for (Node child : children) {
            int maxCandidate = depth(child, newDepth);
            System.out.println(maxCandidate);
            max = Math.max(max, maxCandidate);
        }
        
        return Math.max(max, depth);
    }
}
```



