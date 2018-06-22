# N-ary Tree Preorder Traversal

Given an n-ary tree, return thepreordertraversal of its nodes' values. For example, given a`3-ary`tree:

![](https://leetcode.com/static/images/problemset/NaryTreeExample.png)

  
Return its preorder traversal as:`[1,3,5,6,2,4]`.

**Note: **Recursive solution is trivial, could you do it iteratively?

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
    public List<Integer> preorder(Node root) {
        List<Integer> result = new ArrayList<>();
        traverse(root, result);
        return result;
    }
    
    private void traverse(Node node, List<Integer> result) {
        if (node == null) return;
        result.add(node.val);
        for (Node child : node.children) {
            traverse(child, result);    
        }
    }
}
```



