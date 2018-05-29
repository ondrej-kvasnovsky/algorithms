# Add Binary

Given two binary strings, return their sum \(also a binary string\).

The input strings are both**non-empty**and contains only characters`1`or `0`.

**Example 1:**

```
Input: a = "11", b = "1"
Output: "100"
```

**Example 2:**

```
Input: a = "1010", b = "1011"
Output: "10101"
```

# Solution

```
class Solution {
    public String addBinary(String a, String b) {
        // read from right side (from both strings) until 0
        // convert them to inteteger and add cary, if 3, write 0 and cary 1, if 2 write 0 cary 1, if 1 write 1, else write 0
        List<Character> chars = new ArrayList<>();
        int aIndex = a.length() - 1;
        int bIndex = b.length() - 1;
        int carry = 0;
        while (aIndex >= 0 || bIndex >= 0) {
            
            int aNum = aIndex >= 0 ? (a.charAt(aIndex) - 48) : 0;
            int bNum = bIndex >= 0 ? (b.charAt(bIndex) - 48) : 0;
            int sum = aNum + bNum + carry;
            
            if (sum == 3) {
                chars.add('1');
                carry = 1;
            } else if (sum == 2) {
                chars.add('0');
                carry = 1;
            } else if (sum == 1) {
                chars.add('1');
                carry = 0;
            } else {
                chars.add('0');
                carry = 0;
            }
            
            aIndex--;
            bIndex--;
        }
        if (carry == 1) {
            chars.add('1');
        }
        StringBuilder sb = new StringBuilder();
        for (int i = chars.size() - 1; i >= 0; i--) {
            Character c = chars.get(i);
            sb.append(c);
        }
        return sb.toString();
    }
}
```



