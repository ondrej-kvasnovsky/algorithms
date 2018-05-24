# Longest Substring Without Repeating Characters

Given a string, find the length of the**longest substring**without repeating characters.

**Examples:**

Given`"abcabcbb"`, the answer is`"abc"`, which the length is 3.

Given`"bbbbb"`, the answer is`"b"`, with the length of 1.

Given`"pwwkew"`, the answer is`"wke"`, with the length of 3. Note that the answer must be a**substring**,`"pwke"`is asubsequenceand not a substring.

Here is a solution. 

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        // iterate through letters and put all chars into set, until it is found in the set
        // if found in the set, return cursor to previous start + 1 (i-size) and continue reading from there
        
        int max = 0;
        int count = 0;
        Set<Character> set = new HashSet<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (set.contains(c)) {
                int size = set.size();
                set.clear();
                count = 0;
                i = i - size;
            } else {
                set.add(c);
                count++;
                max = Math.max(max, count);
            }
        }
        
        return max;
    }
}
```



