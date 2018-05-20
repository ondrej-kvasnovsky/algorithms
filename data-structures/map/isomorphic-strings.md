# Isomorphic Strings

Given two strings **s **and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in **s **can be replaced to get **t**.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true
```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false
```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true
```

**Note:**  
You may assume both **s **and **t **have the same length.

First idea was to put characters into hash map with number of occurances and then check if the sizes of the maps are the same. But this does not work for `"aba" "baa"`. The order needs to bee kept. 

```
class Solution {
    public boolean isIsomorphic(String s, String t) {
        // put all chars from s and t into a map that contains char and number of occurances
        // then compare the maps sizes, if the are they same, it is isomorphic, otherwise false
        Map<Character, Integer> sMap = createMap(s);
        Map<Character, Integer> tMap = createMap(t);
        
        return sMap.size() == tMap.size();
    }
    
    private Map<Character, Integer> createMap(String s) {
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char key = s.charAt(i);
            if (map.containsKey(key)) {
                Integer value = map.get(key);
                map.put(key, value + 1);
            } else {
                map.put(key, 1);
            }
        }
        return map;
    }
}
```

Here is a solution. First we check if a value is not in the set, we added. If it is in the set, we compare if it has the same value, if not, we return false. Anyway, it can happen that we don't return false for input 'aa' and 'ba', so we need to add check whether the number of keys and values are the same. If the number of keys are the same, it is isomorphic, but \(like for aa and ba input\) number of keys is 2 and number of values is 1, then the string can't be isomorphic and we have to return false.

```
class Solution {
    public boolean isIsomorphic(String s, String t) {
        // if we store all mappings between letters, there can be no other pairs
        // for 'abb' and 'abb' -> the pairs are -> a:b and b:b (must return true)
        // for 'aba' and 'baa' -> the pairs are -> a:b, b:a and a:a (a:a is wrong - so when we find this case, we return false)
        // for 'ab' and 'aa' -> the pairs are -> a:a and b:a (must return false)
        // for 'ab' and 'ca' -> the pairs are -> a:c and b:a (must return true)
        if (s.length() == 1 && t.length() == 1) {
            return true;
        }
        Map<Character, Character> map = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char sChar = s.charAt(i); // a, b
            char tChar = t.charAt(i); // a, a
            
            System.out.println(map.containsKey(sChar));
            System.out.println(map.containsKey(tChar));
            if (!map.containsKey(sChar)) {
                System.out.println(sChar + ":" + tChar);
                map.put(sChar, tChar);
            } else {
                if (map.get(sChar) != tChar) {
                    return false;
                }
            }
        }
        return new HashSet<>(map.values()).size() == map.size();
    }
}
```



