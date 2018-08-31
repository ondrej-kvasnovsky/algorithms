# First Unique Character in a String

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

**Note: **You may assume the string contain only lowercase letters.

## Solution

```
class Solution {
    public int firstUniqChar(String s) {
        // make counts of each letter (key-value data structure)
        // then go letter by letter and check the number of occurances (if 1, return current index)
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            Integer value = map.getOrDefault(c, 0);
            map.put(c, value + 1);
        }
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            Integer value = map.get(c);
            if (value == 1) {
                return i;
            }
        }
        
        return -1;
    }
}
```



