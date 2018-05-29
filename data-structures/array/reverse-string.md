# Reverse String

Write a function that takes a string as input and returns the string reversed.

**Example:**  
Given s = "hello", return "olleh".

## Solution

```
class Solution {
    public String reverseString(String s) {
        int start = 0;
        int end = s.length() - 1;
        char[] chars = new char[s.length()];
        while (start <= end) {
            char startVal = s.charAt(start);
            char endVal = s.charAt(end);
            chars[start] = endVal;
            chars[end] = startVal;
            start++;
            end--;
        }
        return new String(chars);
    }
}
```



