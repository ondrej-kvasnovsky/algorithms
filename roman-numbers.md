# Roman Numbers 

Roman numerals are represented by seven different symbols: `I`,`V`,`X`,`L`,`C`,`D`and`M`.

```
Symbol        Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

### Roman Numbers to Integer

Lets write code that would convert roman number to an integer. When we first analyze the issue. We find that we can just read the letters and sum their values. But we find that if value is less than the following value, we need to negate it. 

```
I = 1
II = 1 + 1
III = 1 + 1 + 1
IV = 5 - 1 (I is less than V, so we need to change I to -I)
V = 5
```

Here is the code. 

```
class Solution {
    private Map<Character, Integer> mapping = new HashMap<>();

    {
        mapping.put('I', 1);
        mapping.put('V', 5);
        mapping.put('X', 10);
        mapping.put('L', 50);
        mapping.put('C', 100);
        mapping.put('D', 500);
        mapping.put('M', 1000);
    }

    public int romanToInt(String s) {
        int result = 0;

        for (int i = 0; i < s.length(); i++) {
            char current = s.charAt(i);
            Integer currentValue = mapping.get(current);

            if (i < s.length() - 1) {
                char next = s.charAt(i + 1);
                Integer nextValue = mapping.get(next);
                if (nextValue > currentValue) {
                    currentValue = -currentValue;
                }
            }
            result += currentValue;
        }

        return result;
    }
}
```



