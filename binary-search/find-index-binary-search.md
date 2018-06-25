# Binary Search

Given a**sorted**\(in ascending order\) integer array`nums`of`n`elements and a`target`value, write a function to search`target`in`nums`. If`target`exists, then return its index, otherwise return`-1`.  
**Example 1:**

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**

```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

## Solution

```
class Solution {
    public int search(int[] nums, int target) {
        int foundIndex = -1;
        
        int start = 0;
        int end = nums.length - 1;
        
        while (start <= end) {
            // -1, 0, 3, 5, 6
            // -1, 0, 3, 5, 6, 9
            int mid = start + ((end - start) / 2);
            int val = nums[mid];
            if (target < val) {
                end = mid - 1;
            } else if (target > val) {
                start = mid + 1;
            } else {
                foundIndex = mid;
                break;
            }
        }
        
        return foundIndex;
    }
}
```



