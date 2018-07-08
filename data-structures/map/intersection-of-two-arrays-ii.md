# Intersection of Two Arrays II

Given two arrays, write a function to compute their intersection.

**Example:**  
Given: nums1=`[1, 2, 2, 1]`, nums2=`[2, 2]`,  return`[2, 2]`.

And another example:

```
nums1 = [1, 2, 2, 1, 3, 1]
nums2 = [2, 2, 1, 3, 3]
returns [2, 2, 1, 3]
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

**Follow up:**

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

## Solution

Here is a solution.

```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        // iterate through the bigger arra and make counts
        // take the smaller array for comparison to speed it up
        // for each found number, take it, write it into result and decrement by 1
        int[] bigger;
        int[] smaller;
        if (nums1.length > nums2.length) {
            bigger = nums1;
            smaller = nums2;
        } else {
            bigger = nums2;
            smaller = nums1;
        }

        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < bigger.length; i++) {
            int number = bigger[i];
            int count = map.getOrDefault(number, 0);
            map.put(number, count + 1);
        }

        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < smaller.length; i++) {
            int number = smaller[i];
            if (map.containsKey(number)) {
                int count = map.get(number);
                if (count > 0) {
                    result.add(number);
                    map.put(number, count - 1);
                }
            }
        }

        int[] r = result.stream().mapToInt(Integer::intValue).toArray();
        return r;
    }
}
```



