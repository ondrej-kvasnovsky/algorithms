# Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string`""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Note:**

All given inputs are in lowercase letters`a-z`.

## Solution

We could use Trie data structure to do this. First we want to find minimum length of string \(that will tell us max depth of trie tree\). Then we build Trie tree. And then we build max prefix from trie, we create a string until a node 

```
class Solution {

    public String longestCommonPrefix(String[] strs) {
        int min = Integer.MAX_VALUE;
        for (String s : strs) {
            min = Math.min(min, s.length());
        }
        if (min == 0) return "";
        Trie root = new Trie(null);
        for (String s : strs) {
            Trie current = root;
            for (int i = 0; i < min; i++) {
                Character c = s.charAt(i);
                if (current.values.containsKey(c)) {
                    current = current.values.get(c);
                } else {
                    Trie t = new Trie(c);
                    current.values.put(c, t);
                    current = t;
                }
            }
        }
        if (root.values.size() != 1) {
            return "";
        }
        return buildCommonPrefix(root);
    }
    
    private String buildCommonPrefix(Trie node) {
        if (node.values.size() != 1) { // it must be 1, otherwise they split and it is not common prefix
            return String.valueOf(node.value);
        }
        String result = "";
        if (node.value != null) {
            result += node.value;
        }
        result += buildCommonPrefix(node.values.entrySet().iterator().next().getValue());
        return result;
    }
}

class Trie {
    Character value;
    Map<Character, Trie> values = new HashMap<>();
    Trie(Character c) { value = c; }
}
```



