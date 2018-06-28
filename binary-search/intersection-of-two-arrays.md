# Intersection of Two Arrays

Given two arrays, write a function to compute their intersection.

**Example:**  
Given nums1=`[1, 2, 2, 1]`, nums2=`[2, 2]`, return`[2]`.

## Solution

Time complexity O\(n\). 

```
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        // iterate through the first array and add it into set (to ensure unique values)
        // then iterate through second array and if the value is contained, it is intersection
        // than move data from set into array and retur it back
        Set<Integer> values = new HashSet<>();
        for (int num : nums1) {
            values.add(num);
        }
        Set<Integer> intersections = new HashSet<>();
        for (int num : nums2) {
            if (values.contains(num)) {
                intersections.add(num);
            }
        }
        int[] result = new int[intersections.size()];
        int index = 0;
        for (Integer num : intersections) {
            result[index++] = num;
        }
        return result;
    }
}
```

Sort both arrays, use two pointers. Time complexity: O\(n log n\)

```
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0;
        int j = 0;
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] < nums2[j]) {
                i++;
            } else if (nums1[i] > nums2[j]) {
                j++;
            } else {
                set.add(nums1[i]);
                i++;
                j++;
            }
        }
        int[] result = new int[set.size()];
        int k = 0;
        for (Integer num : set) {
            result[k++] = num;
        }
        return result;
    }
}
```

Binary search. Time complexity: O\(n log n\)

```
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums2);
        for (Integer num : nums1) {
            if (binarySearch(nums2, num)) {
                set.add(num);
            }
        }
        int i = 0;
        int[] result = new int[set.size()];
        for (Integer num : set) {
            result[i++] = num;
        }
        return result;
    }
    
    public boolean binarySearch(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return false;
    }
}
```



