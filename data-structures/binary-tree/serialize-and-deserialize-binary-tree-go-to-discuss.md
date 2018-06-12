# Serialize and Deserialize Binary Tree

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Example: **

```
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "[1,2,3,null,null,4,5]"
```

**Clarification:**The above format is the same as[how LeetCode serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note: **Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

## Solution

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) return null;
        // 0, 1, 2, 3, 4
        // 1, 2, 3, 4, 5
        // root             => 2 * 0 = 0
        // root.left        => 2 * 0 + 1 = 1
        // root.right       => 2 * 0 + 2 = 2
        // root.left.left   => 2 * 1 + 1 = 3
        // root.left.right  => 2 * 1 + 2 = 4
        // root.right.left  => 2 * 2 + 1 = 5
        // root.right.right => 2 * 2 + 2 = 6
        // read root, and append its value plus values of left and right
        // do the same for left and right
        // then the same for left.left and left.right
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                sb.append("null,");
                continue;
            }
            sb.append(node.val);
            sb.append(",");
            queue.offer(node.left);
            queue.offer(node.right);
        }
        String result = sb.toString();
        System.out.println(result);
        return result.substring(0, result.length() - 1);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null) return null;
        String[] split = data.split(",");
        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode root = new TreeNode(Integer.valueOf(split[0]));
        queue.offer(root);
        int index = 1;
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            // add left
            String leftValue = split[index++];
            if (!"null".equals(leftValue)) {
                TreeNode left = new TreeNode(Integer.valueOf(leftValue));
                node.left = left;
                queue.offer(left);
            }
            
            // add right
            String rightValue = split[index++];
            if (!"null".equals(rightValue)) {
                TreeNode right = new TreeNode(Integer.valueOf(rightValue));
                node.right = right;
                queue.offer(right);
            }
        }
        
        
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```



