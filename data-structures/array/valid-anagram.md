# Valid Anagram

Given two strings _s _and _t_, write a function to determine if _t _is an anagram of _s_.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

**Note:**  
You may assume the string contains only lowercase alphabets.

## Solution

One idea is to sort both strings and then compare them. That would give us O\(n log n\) time complexity.

```
class Solution {
    public boolean isAnagram(String s, String t) {
        char[] sChars = s.toCharArray();
        char[] tChars = t.toCharArray();
        Arrays.sort(sChars);
        Arrays.sort(tChars);
        return new String(sChars).equals(new String(tChars));
    }
}
```

Another idea could be to make a map that contains all letters and its counts of _s_ string. Then do the same for  _t_. Then compare whether these sets are the same. That would give us O \(n\) time complexity.

```
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        
        Map<Character, Integer> sMap = getCounts(s);
        Map<Character, Integer> tMap = getCounts(t);
        if (sMap.size() != tMap.size()) {
            return false;
        }
        
        for (char c : t.toCharArray()) {
            Integer sValue = sMap.get(c);
            Integer tValue = tMap.get(c);
            if (sValue == null || !sValue.equals(tValue)) {
                return false;
            }
        }
        return true;
    }
    
    private Map<Character, Integer> getCounts(String s) {
        Map<Character, Integer> counts = new HashMap<>();
        for (char c : s.toCharArray()) {
            Integer value = counts.getOrDefault(c, 0);
            counts.put(c, value + 1);
        }
        return counts;
    }
}
```



