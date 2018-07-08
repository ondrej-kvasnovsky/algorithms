# Plus One

Given a **non-empty **array of digits representing a non-negative integer, plus one to the integer.

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

## Solution

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

Or we can create the new array and put it all there from the beginning.

```
class Solution {
    public int[] plusOne(int[] digits) {
        // [1] = [2]
        // [1, 1] = [1, 2] -> take increase number on last position, if i tis higher than 10, then substract 10 and put remaining to some temp variable, then do the other iteration only if remaining is not 0

        // increment last value by one
        // iterate through array from end
        // init carry = 0
        // get last value 
        // increment the last value
        // if >= 10 -> carry = 1 and value - 10, add value to stack
        // else add value to stack

        // take items from stack and put them into new array of stack size

        int[] result = new int[digits.length + 1];
        digits[digits.length - 1]++;
        int carry = 0;
        for (int i = digits.length - 1; i >= 0; i--) {
            int value = digits[i];
            if (carry == 1) {
                value++;
                carry = 0;
            }
            if (value >= 10) {
                carry = 1;
                value -= 10;
            }
            result[i + 1] = value;
        }
        if (carry == 1) {
            result[0] = 1;
        } else {
            int[] smaller = new int[digits.length];
            System.arraycopy(result, 1, smaller, 0, smaller.length);
            return smaller;
        }
        return result;
    }
}
```



