# Find Minimum in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand. \(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`\). Find the minimum element. You may assume no duplicate exists in the array.

**Example 1:**

```
Input: [3,4,5,1,2] 
Output: 1
```

**Example 2:**

```
Input: [4,5,6,7,0,1,2]
Output: 0
```

## Solution

```
class Solution {
    public int findMin(int[] nums) {
        int start = 0;
        int end = nums.length - 1;
        
        while (start < end) {
            // options
            // [4,5,6,7,0,1,2] or [1,2,4,5,6,7,0] or [7,0,1,2,4,5,6] or [0,1,2,4,5,6,7]
            // min?
            int mid = start + (end - start) / 2;
            
            if (nums[mid] > nums[end]) { // 2,3,1
                start = mid + 1; // move start to position 2
            } else {
                // 6,7,0,1,2
                // move end position to middle, to position 2
                end = mid;
            }
        }
        
        return nums[start];
    }
}
```



