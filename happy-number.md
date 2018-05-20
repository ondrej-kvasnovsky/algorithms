# Happy Number

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 \(where it will stay\), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

```
Input: 19
Output: true
Explanation: 
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

Here is a solution.

```
class Solution {
    public boolean isHappy(int n) {
        // 1 is happy number
        // 10 is happy number
        // 100 is happy number
        // 20 -> 4 + 0 (40) -> 16 + 0 (16) -> 1 + 36 + 0 (37) -> 9 + 49 + 0 (58) -> ...
        Set<Integer> set = new HashSet<>();

        int current = n;
        while (set.add(current)) {
            current = sum(current);
            if (current == 1) {
                return true;
            }
        }
        return current == 1;
    }

    private int sum(int n) {
        // parsing string and casting chars might be slowing down the algorighm
        // int[] values = String.valueOf(n)
        //     .chars()
        //     .map(Character::getNumericValue)
        //     .toArray();
        int sum = 0;
        while (n > 0) {
            int value = n % 10;
            int m = value * value;
            sum += m;
            n = n / 10;
        }
        return sum;
    }
}
```



