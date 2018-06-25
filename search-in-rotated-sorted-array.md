# Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`[0,1,2,4,5,6,7]`might become`[4,5,6,7,0,1,2]`\).

You are given a target value to search. If found in the array return its index, otherwise return`-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of _O_\(log _n_\).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

## Solution

```
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            int midVal = nums[mid];
            if (target == midVal) {
                return mid;
            }
            int lowVal = nums[low];
            if (midVal < lowVal) { // if middle is less than lowest value
                // 6,7,0,1,2,3,4,5
                if (target < midVal || target >= lowVal) { 
                    // and target is less than middle or target is bigger than lowest value, move high closer to left side (e.g. target=7)
                    high = mid - 1;
                } else {
                    // e.g. target=5
                    low = mid + 1;
                }
            } else {
                // 2,3,4,5,6,7,0,1
                if (target > midVal || target < lowVal) {
                    // target is e.g. 6
                    low = mid + 1;
                } else {
                    // target is e.g. 2
                    high = mid - 1;
                }
            }
        }
        return -1;
    }
}
```



