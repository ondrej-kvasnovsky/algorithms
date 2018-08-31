# Plus One

Given a **non-empty **array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

**Example 1:**

```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example 2:**

```
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

  
Solution

```
class Solution {
    public int[] plusOne(int[] digits) {
        // add 1 to the last, if result is bigger than 9, substract 10 (and put this value into that position), and remember one
        // add 1 to the another one + the remembered number
        int remaining = 0;
        digits[digits.length - 1]++;
        for (int i = digits.length - 1; i >= 0; i--) {
            int num = digits[i] + remaining;
            if (num > 9) {
                remaining = 1;
                num = num - 10;
            } else {
                remaining = 0;
            }
            digits[i] = num;
        }
        if (remaining == 1) {
            int[] newArray = new int[digits.length + 1];
            newArray[0] = 1;
            System.arraycopy(digits, 0, newArray, 1, digits.length);
            return newArray;
        }
        
        return digits;
    }
}
```



