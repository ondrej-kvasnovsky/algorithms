# Count and Say

The count-and-say sequence is the sequence of integers with the first five terms as following:

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1`is read off as`"one 1"`or`11`.  
`11`is read off as`"two 1s"`or`21`.  
`21`is read off as`"one 2`, then`one 1"`or`1211`.

Given an integern, generate thenthterm of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

```
Input: 1
Output: "1"
```

**Example 2:**

```
Input: 4
Output: "1211"
```

## Solution

```
class Solution {
    // 1 -> 11 -> 21 -> 1211 -> 111221 -> 312211 -> 1311...
    // count all numbers until they are the same, then write how many of the same nunbers you got
    // create loop fro 0 to n-1
    // express the current value of 1 -> look at the number and check the next number -> if not, write how many times you got this number
    public String countAndSay(int n) {
        StringBuilder init = new StringBuilder();
        init.append(1);
        if (n == 1) {
            return init.toString();
        }
        
        String result = "";
        for (int i = 0; i < n - 1; i++) {
            String newItem = generate(init);
            init = new StringBuilder(newItem);
            result = init.toString();
        }
        return result;
    }
    
    public String generate(StringBuilder builder) {
        StringBuilder newSequence = new StringBuilder();
        String s = builder.toString();
        int howManyTimes = 1;
        for (int i = 0; i < s.length(); i++) {
            char current = s.charAt(i);
            char next = ' ';
            if (i + 1 < s.length()) {
                next = s.charAt(i + 1);
            }
            if (current == next) {
                howManyTimes++;
            } else {
                // write how many times & what
                newSequence.append(howManyTimes);
                newSequence.append(current);
                howManyTimes = 1;
            }
        }
        return newSequence.toString();
    }
}


```



