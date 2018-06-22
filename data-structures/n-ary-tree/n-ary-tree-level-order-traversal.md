# N-ary Tree Level Order Traversal

Given an n-ary tree, return the level order traversal of its nodes' values. \(ie, from left to right, level by level\). For example, given a`3-ary`tree:

![](https://leetcode.com/static/images/problemset/NaryTreeExample.png)

We should return its level order traversal:

```
[
     [1],
     [3,2,4],
     [5,6]
]
```

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
    public List<List<Integer>> levelOrder(Node root) {
        return traverse(root);
    }
    
    private List<List<Integer>> traverse(Node node) {
        List<List<Integer>> result = new ArrayList<>();
        if (node == null) return result;
        
        Queue<Node> queue = new LinkedList<>();
        queue.offer(node);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> subList = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                Node current = queue.poll();
                subList.add(current.val);
                if (current.children != null) {
                    for (Node child : current.children) {
                        queue.offer(child);
                    }
                }
            }
            result.add(subList);
        }
        return result;
    }
}
```



