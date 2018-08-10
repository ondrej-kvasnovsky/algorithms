# Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output: 321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

One solution is to convert number to string and then handle trailing 0s. Anyway, here is a solution that uses division and multiplication.

```
class Solution {
    public int reverse(int x) {
        if (x == 0) return 0;
        boolean isNegative = false;
        if (x < 0) {
            x = -x;
            isNegative = true;
        }
        int reversed = 0;
        int prev_reversed = 0;
        while (x > 0) {
            reversed = reversed * 10 + x % 10;
            if (reversed / 10 != prev_reversed) return 0;
            prev_reversed = reversed;
            x /= 10;
        }

        return isNegative ? -reversed : reversed;
    }
}
```



