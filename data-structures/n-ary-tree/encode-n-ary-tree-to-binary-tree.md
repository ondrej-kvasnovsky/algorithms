# Encode N-ary Tree to Binary Tree

Design an algorithm to encode an N-ary tree into a binary tree and decode the binary tree to get the original N-ary tree. An N-ary tree is a rooted tree in which each node has no more than N children. Similarly, a binary tree is a rooted tree in which each node has no more than 2 children. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that an N-ary tree can be encoded to a binary tree and this binary tree can be decoded to the original N-nary tree structure.

For example, you may encode the following`3-ary`tree to a binary tree in this way:![](https://leetcode.com/static/images/problemset/NaryTreeBinaryTreeExample.png)

Note that the above is just an example which_might or might not_work. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:**

1. `N `is in the range of `[1, 1000]`
2. Do not use class member/global/static variables to store states. Your encode and decode algorithms should be stateless.

## Solution

There are a lot of solutions to convert a N-ary tree to a binary tree. We only introduce one classical solution.

The strategy follows two rules:

1. The`left child`of each node in the binary tree is`the next sibling`of the node in the N-ary tree.
2. The`right child`of each node in the binary tree is`the first child`of the node in the N-ary tree.

Using this strategy, you can convert a N-ary tree to a binary tree recursively. Also, you can recover the N-ary tree from the binary tree you converted.

The recursion recovery strategy for each node is:

1. Deal with its children recursively.
2. Add its`left child`as`the next child of its parent`if it has a left child.
3. Add its`right child`as`the first child of the node itself`if it has a right child.



