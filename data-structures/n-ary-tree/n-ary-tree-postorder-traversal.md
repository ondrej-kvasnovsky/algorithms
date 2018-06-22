# N-ary Tree Postorder Traversal

Given an n-ary tree, return thepostordertraversal of its nodes' values. For example, given a`3-ary`tree:

![](https://leetcode.com/static/images/problemset/NaryTreeExample.png)

Return its postorder traversal as:`[5,6,3,2,4,1]`.

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
    public List<Integer> postorder(Node root) {
        List<Integer> result = new ArrayList<>();
        traverse(root, result);
        return result;
    }
    
    private void traverse(Node node, List<Integer> result) {
        if (node == null) return;
        for (Node child : node.children) {
            traverse(child, result);    
        }
        result.add(node.val);
    }
}
```



