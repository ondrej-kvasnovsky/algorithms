# Search in a Sorted Array of Unknown Size

Given an integer array sorted in ascending order, write a function to search`target`in`nums`.  If`target`exists, then return its index, otherwise return`-1`. **However, the array size is unknown to you**. You may only access the array using an`ArrayReader` interface, where `ArrayReader.get(k)`returns the element of the array at index`k` \(0-indexed\).

You may assume all integers in the array are less than `10000`, and if you access the array out of bounds,`ArrayReader.get`will return`2147483647`.

**Example 1:**

```
Input: array = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

```

**Example 2:**

```
Input: array = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

## Solution

First find the last valid value \(a value which is not 2147483647\). Then repeat binary search from 0 to the last found index. 

```
class Solution {
    public int search(ArrayReader reader, int target) {
        if (reader == null) {
            return -1;
        }
        
        int lastElement = -1;
        int left = 0;
        int right = 9999;
        while (left <= right) {
            int mid = left + ((right - left) / 2);
            int value = reader.get(mid);
            if (value == 2147483647) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        lastElement = left;
        
        int start = 0;
        int end = lastElement;
        while (start <= end) {
            int middle = start + ((end - start) / 2);
            int val = reader.get(middle);
            if (val == target) {
                return middle;
            } else if (target > val) {
                start = middle + 1;
            } else {
                end = middle - 1;
            }
        }
        
        return -1;
    }
}
```



