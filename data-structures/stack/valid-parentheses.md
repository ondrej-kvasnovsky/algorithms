# Valid Parentheses

Given a string containing just the characters`'('`,`')'`,`'{'`,`'}'`,`'['`and`']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

```
Example 1:

Input: "()"
Output: true

Example 2:

Input: "()[]{}"
Output: true

Example 3:

Input: "(]"
Output: false

Example 4:

Input: "([)]"
Output: false

Example 5:

Input: "{[]}"
Output: true
```

## Solution

Here is a solution using stack.

```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) {
                    return false;
                }
                char previous = stack.pop();
                if (previous == '(') {
                    if (c != ')')
                        return false;
                }
                if (previous == '[') {
                    if (c != ']')
                        return false;
                }
                if (previous == '{') {
                    if (c != '}')
                        return false;
                }
            }
        }

        return stack.isEmpty();
    }
}
```



