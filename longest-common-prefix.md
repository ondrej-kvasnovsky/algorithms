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

Here is a solution.

```
class Solution {

    public String onlyCommonPrefix(String s1, String s2) {
        String s = "";
        int i = 0;
        int j = 0;
        while (j < s1.length() || j < s2.length()) {
            String c1 = "";
            if (j < s1.length()) {
                c1 = s1.substring(i, i + 1);
            }
            String c2 = "";
            if (j < s2.length()) {
                c2 = s2.substring(j, j + 1);
            }
            if (c1.equals(c2)) {
                s += c1;
            } else {
                break;
            }
            i++;
            j++;
        }
        return s;
    }

    public String longestCommonPrefix(String[] strs) {
        String commonPrefix = null;
        for (String s : strs) {
            if (commonPrefix == null) {
                commonPrefix = s;
            }
            commonPrefix = onlyCommonPrefix(commonPrefix, s);
        }
        return commonPrefix == null ? "" : commonPrefix;
    }
}
```

We could add minimum length as constrain, so we don't iterate through all the letters.

```
class Solution {
    public String onlyCommonPrefix(String s1, String s2, int min) {
        String s = "";
        int i = 0;
        int j = 0;
        while (j < s1.length() || j < s2.length())  {
            String c1 = "";
            if (j < s1.length()) {
                c1 = s1.substring(i, i + 1);
            }
            String c2 = "";
            if (j < s2.length()) {
                c2 = s2.substring(j, j + 1);
            }
            if (c1.equals(c2)) {
                s += c1;
            } else {
                break;
            }
            i++;
            j++;
            if (j >= min && j >= min) {
                break;
            }
        }
        return s;
    }

    public String longestCommonPrefix(String[] strs) {
        int min = Integer.MAX_VALUE;
        for (String s : strs) {
            min = Math.min(min, s.length());
        }
        
        String commonPrefix = null;
        for (String s : strs) {
            if (commonPrefix == null) {
                commonPrefix = s;
            }
            commonPrefix = onlyCommonPrefix(commonPrefix, s, min);
        }
        return commonPrefix == null ? "" : commonPrefix;
    }
}
```

Another option would be to use trie data structure. Put all the letters there \(up to min length from previous example\). Then get couple of letters from top \(until some node has multiple nodes\).

```
class Solution {

    public String longestCommonPrefix(String[] strs) {
        int min = Integer.MAX_VALUE;
        for (String s : strs) {
            min = Math.min(min, s.length());
        }
        
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
        if (node.values.size() != 1) {
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



