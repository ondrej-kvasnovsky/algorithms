# Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**

```
Input: "A man, a plan, a canal: Panama"
Output: true
```

**Example 2:**

```
Input: "race a car"
Output: false
```

## Solution

```
import java.lang.StringBuilder;

class Solution {
    public boolean isPalindrome(String s) {
        String connected = s.toLowerCase().replaceAll("[^a-z0-9]", "");

        for (int i = 0, j = connected.length() - 1; i < j; i++, j--) {
            char c1 = connected.charAt(i);
            char c2 = connected.charAt(j);
            if (c1 != c2) {
                return false;
            }
        }

        return true;
    }
}
```



