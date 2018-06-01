# Reverse Words in a String III

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**

```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

**Note:**In the string, each word is separated by single space and there will not be any extra space in the string.

## Solution

```
class Solution {
    public String reverseWords(String s) {
        String[] split = s.split(" ");
        StringBuilder builder = new StringBuilder();
        for (int i = 0; i < split.length; i++) {
            builder.append(flip(split[i]));
            if (i != split.length - 1) {
                builder.append(" ");
            }
        }
        return builder.toString();
    }
    
    private String flip(String s) {
        StringBuilder builder = new StringBuilder();
        for (int i = s.length() - 1; i >= 0; i--) {
            builder.append(s.charAt(i));
        }
        return builder.toString();
    }
}
```

Another idea is to make thow builders, one for the whole sentense the another for each word, when empty space is found, write work an the empty space. 

