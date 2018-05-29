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







