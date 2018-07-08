# Implement strStr\(\)

Implement [strStr\(\)](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1 **if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

**Clarification:**

What should we return when`needle`is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when`needle`is an empty string. This is consistent to C's [strstr\(\)](http://www.cplusplus.com/reference/cstring/strstr/) and Java's  [indexOf\(\)](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf%28java.lang.String%29).

## Solution

```
class Solution {
    // "aaaaa", "b" => -1
    // "aaaaa", "a" => 0
    // "aa", "aa" => 0
    // hello, ll => 2
    public int strStr(String haystack, String needle) {
        int index = -1;
        if (needle == null || haystack == null) {
            return index;
        }
        if (needle.length() > haystack.length()) {
            return index;
        }
        if (needle.equals(haystack)) {
            return 0;
        }

        for (int i = 0; i < haystack.length(); i++) {
            if (i + needle.length() <= haystack.length()) {
                // for example: hello & ll
                // 2 + 2 <= 5, try to compare substring(2, 2 + 2) == needle
                if (haystack.substring(i, i + needle.length()).equals(needle)) {
                    return i;
                }    
            }
        }
        return index;
    }
}
```



