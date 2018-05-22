# Group Anagrams

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

* All inputs will be in lowercase.
* The order of your output does not matter.

Here is a solution using hash map.

```
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        // sort string, and use it as key, then put it into hash map (key = sorted string, value is list of Stings)
        Map<String, List<String>> map = new HashMap<>();
        for (String s : strs) {
            char[] c = s.toCharArray();
            Arrays.sort(c);
            String sorted = new String(c);
            List<String> list = map.getOrDefault(sorted, new ArrayList<>());
            list.add(s);
            map.put(sorted, list);
        }

        List<List<String>> result = new ArrayList<>();
        Iterator<List<String>> iterator = map.values().iterator();
        while(iterator.hasNext()) {
            result.add(iterator.next());
        }
        return result;
    }
}
```

Other solution might be to compile string into numerical string. First we would count all the letters, how many times they occur in the string? For example, "aab" would become a:2, b:1. Then we would create a template that would consist from all the letters \(lets say only lower case is used\): \`2:1::::::::::::::::\`. Then we can use these strings as a keys. 

