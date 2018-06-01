# Reverse Words in a String

Given an input string, reverse the string word by word.

**Example:  **

```
Input: "the sky is blue",
Output: "blue is sky the".
```

**Note:**

* A word is defined as a sequence of non-space characters.
* Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
* You need to reduce multiple spaces between two words to a single space in the reversed string.

## Solution

```
public class Solution {
    public String reverseWords(String s) {
        String[] split = s.split(" ");
        StringBuilder builder = new StringBuilder();
        for (int i = split.length - 1; i >= 0; i--) {
            if ("".equals(split[i])) continue;
            builder.append(split[i]);
            if (i != 0) {
                builder.append(" ");
            }
        }
        return builder.toString().trim();
    }
}
```



