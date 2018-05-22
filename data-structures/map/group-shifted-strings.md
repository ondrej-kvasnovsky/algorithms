# Group Shifted Strings

Given a string, we can "shift" each of its letter to its successive letter, for example:`"abc" -> "bcd"`. We can keep "shifting" which forms the sequence:

```
"abc" -> "bcd" -> ... -> "xyz"
```

Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

**Example:**

```
Input: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"],
Output: 
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
```

Here is a solution.

```
class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        Map<String, List<String>> map = new HashMap<>();
        for (String s : strings) {
            StringBuilder sb = new StringBuilder();
            char[] chars = s.toCharArray();
            int shift = 'z' - chars[0];
            System.out.println("Shift: " + shift);
            for (char c : chars) {
                System.out.println("Letter: " + (int) c);
                int normalized = (c + shift) % 26;
                System.out.println("Normalized: " + normalized);
                sb.append(normalized);
            }
            String key = sb.toString();
            System.out.println("Key: " + key);
            List<String> list = map.getOrDefault(key, new ArrayList<>());
            list.add(s);
            map.put(key, list);
            System.out.println();
        }

        return new ArrayList<>(map.values());
    }
}
```

Here is the output for better understanding what is happening \(how shifting is done and how to normalize it\).

```
Your input
["abc","bcd","acef","xyz","az","ba","a","z"]

Your stdout
Shift: 25
Letter: 97
Normalized: 18
Letter: 98
Normalized: 19
Letter: 99
Normalized: 20
Key: 181920

Shift: 24
Letter: 98
Normalized: 18
Letter: 99
Normalized: 19
Letter: 100
Normalized: 20
Key: 181920

Shift: 25
Letter: 97
Normalized: 18
Letter: 99
Normalized: 20
Letter: 101
Normalized: 22
Letter: 102
Normalized: 23
Key: 18202223

Shift: 2
Letter: 120
Normalized: 18
Letter: 121
Normalized: 19
Letter: 122
Normalized: 20
Key: 181920

Shift: 25
Letter: 97
Normalized: 18
Letter: 122
Normalized: 17
Key: 1817

Shift: 24
Letter: 98
Normalized: 18
Letter: 97
Normalized: 17
Key: 1817

Shift: 25
Letter: 97
Normalized: 18
Key: 18

Shift: 0
Letter: 122
Normalized: 18
Key: 18

Your answer
[["az"],["abc","bcd","xyz"],["acef"],["a","z"],["ba"]]
```



