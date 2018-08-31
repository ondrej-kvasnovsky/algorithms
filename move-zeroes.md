# Move Zeroes

Given an array`nums`, write a function to move all`0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place **without making a copy of the array.
2. Minimize the total number of operations.

## Solution

```
class Solution {
    public void moveZeroes(int[] nums) {
        int current = 0;
        int lastNotZeroIndex = 0;
        
        while (current < nums.length) {
            int num = nums[current];
            if (num != 0) {
                nums[current] = nums[lastNotZeroIndex];
                nums[lastNotZeroIndex] = num;    
                lastNotZeroIndex++;
            }
            
            current++;
        }
    }
}
```



