# Intersection of Two Arrays

Given two arrays, write a function to compute their intersection.

Example:

```
Given
nums1=[1, 2, 2, 1],
nums2=[2, 2], 
return[2].
```

**Note:**

* Each element in the result must be unique.
* The result can be in any order.

Here is a solution that uses sets to get unique elements.

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



