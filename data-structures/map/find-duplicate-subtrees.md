## Find Duplicate Subtrees

Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any **one **of them.

Two trees are duplicate if they have the same structure with same node values.

**Example 1:**

```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```

The following are two duplicate subtrees:

```
      2
     /
    4
```

and

```
    4
```

Therefore, you need to return above trees' root in the form of a list.

Here is a solution. 

```
class Solution {
    private final List<TreeNode> duplicates = new ArrayList<>();
    
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        // a node in a binary tree is: node, node.left and node.right
        // we need to iterate through the nodes and build key for each node, then as we are building the keys and a hash map, we check for duplicate keys, if duplicate key is found, we add that node into list
        // 1 -> 2 ->null,null
        // 1 -> 2 ->null,null
        find(root);
        return duplicates;
    }
    
    private Map<String, Integer> keys = new HashMap<>();
    
    public String find(TreeNode node) {
        if (node == null) return "-";
        String key = String.valueOf(node.val) + find(node.left) + find(node.right);
        System.out.println(key);
        if (keys.containsKey(key) && keys.get(key) == 0) {
            System.out.println("adding...");
            duplicates.add(node);
            keys.put(key, 1);
        } else {
            if (!keys.containsKey(key)) {
                keys.put(key, 0);
            }
        }
        return key;
    }
}
```



