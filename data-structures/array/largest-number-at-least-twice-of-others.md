# Largest Number At Least Twice of Others

In a given integer array`nums`, there is always exactly one largest element.

Find whether the largest element in the array is at least twice as much as every other number in the array.

If it is, return the**index**of the largest element, otherwise return -1.

**Example 1:**

```
Input: nums = [3, 6, 1, 0]
Output: 1
Explanation: 6 is the largest integer, and for every other number in the array x,
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.
```

**Example 2:**

```
Input: nums = [1, 2, 3, 4]
Output: -1
Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.
```

**Note:**

1. `nums`will have a length in the range`[1, 50]`.
2. Every`nums[i]`will be an integer in the range`[0, 99]`.

# Solution

First idea is to find max and then check if double of all the numbers \(except max\) are less or equal to the max number.

```
class Solution {
    public int dominantIndex(int[] nums) {
        if (nums.length == 1) {
            return 0;
        }
        // 1 idea
        // first iteration, find max
        // second iteration, find if max / current value is 2 or less (if yes, return 1)
        int max = Integer.MIN_VALUE;
        int maxIndex = -1;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > max) {
                maxIndex = i;
                max = nums[i];
            }
        }
        
        boolean isDouble = false;
        for (int i = 0; i < nums.length; i++) {
            if (i == maxIndex) continue;
            int num = nums[i];
            boolean isLess = num == 0 || num * 2 <= max;
            if (isLess) {
                isDouble = true;
            } else {
                isDouble = false;
                break;
            }
        }
        if (isDouble) {
            return maxIndex;
        }
        return -1;
    }
}
```



