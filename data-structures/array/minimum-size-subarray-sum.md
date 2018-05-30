# Minimum Size Subarray Sum

Given an array of**n**positive integers and a positive integer**s**, find the minimal length of a**contiguous**subarray of which the sum ≥**s**. If there isn't one, return 0 instead.

**Example: **

```
Input: [2,3,1,2,4,3], s = 7
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

## Solution

```
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        // make window, if sum exceeds the 's', then move start, otherwise, in each iteration move end
        int start = 0;
        int end = 0;
        int min = Integer.MAX_VALUE;
        while (start <= end && end < nums.length) {
            int sum = sum(nums, start, end); // this could be optimized, only keep sum and when start++, substract start value from it
            if (sum >= s) {
                min = Math.min(min, end - start + 1);
            }
            if (sum > s) {
                start++;
            } else {
                end++;    
            }
        }
        if (min == Integer.MAX_VALUE) {
            return 0;
        }
        return min;
    }

    private int sum(int[] nums, int start, int end) {
        int sum = 0;
        for (int i = start; i <= end; i++) {
            sum += nums[i];
        }
        return sum;
    }
}
```

Here is the optimized solution. 

```
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int min = Integer.MAX_VALUE;
        
        int start = 0;
        int end = 0;
        
        int sum = 0;
        while (start <= end && end <= nums.length) {
            if (sum > s) {
                sum -= nums[start];
                start++;
            } else {
                if (end == nums.length) break;
                sum += nums[end];
                end++;  
            }
            if (sum >= s) {
                min = Math.min(min, end - start);
            }

        }
        if (min == Integer.MAX_VALUE) {
            return 0;
        }
        return min;
    }
}
```



