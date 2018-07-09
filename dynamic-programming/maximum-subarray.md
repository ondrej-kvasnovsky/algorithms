# Maximum Subarray

Given an integer array`nums`, find the contiguous subarray \(containing at least one number\) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O\(_n_\) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## Solution

First attempt solution, but it is dead end because of time complexity. 

```
class Solution {
    public int maxSubArray(int[] nums) {
        // 1.
        // [1, -2] -> 0, 0 -> 1 > -... yes, max = 1, move end++, 0, 1 -> -1 > 1 no, so 1
        // [-2, 1, -3-, 4], 0, 0 -> -2, 0, 1 -> -1 - start++, 1, 1 -> 1 yes, end++
        // two pointers, start = 0; end = 0
        // max sum = Integer.MIN_VALUE
        // current sum = sum(nums, start, end)
        // if (current > max) max = current
        // else, increment end
        int start = 0;
        int end = 0;
        int max = Integer.MIN_VALUE;
        
        while(start < nums.length && end < nums.length) {
           int sum = sum(nums, start, end);
           if (sum > max) {
               max = sum;
           } else {
               start++;
           }
            end++;
        }
        return max;
    }
    
    public int sum(int[] nums, int start, int end) {
        int sum = nums[start];
        int i = start + 1;
        while (i <= end) {
            sum += nums[i];
            i++;
        }
        return sum;
    }
}
```

Other solution.

```
class Solution {
    public int maxSubArray(int[] nums) {
        // 2.
        // start with 0th element as current value and max value
        int max = nums[0];
        int currentMax = nums[0];
        // get objective, find the max subarray value
        for (int i = 1; i < nums.length; i++) {
            // if current is bigger than what we gathered, we can contine
            currentMax = Math.max(nums[i], currentMax + nums[i]);
            max = Math.max(max, currentMax);
        }
        
        return max;
    }
}
```

Here is a solution using dynamic programming. It is not faster, but it is interesting as well. 

```
class Solution {
    public int maxSubArray(int[] nums) {
        //3. 
        int n = nums.length;
        int[] temp = new int[n];//dp[i] means the maximum subarray ending with A[i];
        temp[0] = nums[0];
        int max = temp[0];
        
        for(int i = 1; i < n; i++) {
            temp[i] = nums[i];
            if (temp[i - 1] > 0) {
                temp[i] += temp[i - 1];
            }
            max = Math.max(max, temp[i]);
            System.out.println(Arrays.toString(temp));
        }
        
        return max;
    }
}
```

Here is the sample input and output. 

```
Input: [-2,1,-3,4,-1,2,1,-5,4]

System out: 
[-2, 1, 0, 0, 0, 0, 0, 0, 0]
[-2, 1, -2, 0, 0, 0, 0, 0, 0]
[-2, 1, -2, 4, 0, 0, 0, 0, 0]
[-2, 1, -2, 4, 3, 0, 0, 0, 0]
[-2, 1, -2, 4, 3, 5, 0, 0, 0]
[-2, 1, -2, 4, 3, 5, 6, 0, 0]
[-2, 1, -2, 4, 3, 5, 6, 1, 0]
[-2, 1, -2, 4, 3, 5, 6, 1, 5]

Answer is: 6
```



