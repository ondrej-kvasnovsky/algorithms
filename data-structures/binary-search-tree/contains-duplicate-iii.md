# Contains Duplicate III

Given an array of integers, find out whether there are two distinct indicesiandjin the array such that the**absolute**difference between**nums\[i\]**and**nums\[j\]**is at mosttand the**absolute**difference betweeniandjis at mostk.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3, t = 0
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1, t = 2
Output: true
```

**Example 3:**

```
Input: nums = [1,5,9,1,5,9], k = 2, t = 3
Output: false
```

## Solution

Solution that would take a lot of time. 

```
public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    for (int i = 0; i < nums.length; ++i) {
        for (int j = Math.max(i - k, 0); j < i; ++j) {
            if (Math.abs(nums[i] - nums[j]) <= t) return true;
        }
    }
    return false;
}
```

More optimized solution using binary search tree. 

```
public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    TreeSet<Integer> set = new TreeSet<>();
    for (int i = 0; i < nums.length; ++i) {
        // Find the successor of current element
        Integer s = set.ceiling(nums[i]);
        if (s != null && s <= nums[i] + t) return true;

        // Find the predecessor of current element
        Integer g = set.floor(nums[i]);
        if (g != null && nums[i] <= g + t) return true;

        set.add(nums[i]);
        if (set.size() > k) {
            set.remove(nums[i - k]);
        }
    }
    return false;
}
```

Solution using buckets. 

    public class Solution {
        // Get the ID of the bucket from element value x and bucket width w
        // In Java, `-3 / 5 = 0` and but we need `-3 / 5 = -1`.
        private long getID(long x, long w) {
            return x < 0 ? (x + 1) / w - 1 : x / w;
        }

        public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
            if (t < 0) return false;
            Map<Long, Long> d = new HashMap<>();
            long w = (long)t + 1;
            for (int i = 0; i < nums.length; ++i) {
                long m = getID(nums[i], w);
                // check if bucket m is empty, each bucket may contain at most one element
                if (d.containsKey(m))
                    return true;
                // check the neighbor buckets for almost duplicate
                if (d.containsKey(m - 1) && Math.abs(nums[i] - d.get(m - 1)) < w)
                    return true;
                if (d.containsKey(m + 1) && Math.abs(nums[i] - d.get(m + 1)) < w)
                    return true;
                // now bucket m is empty and no almost duplicate in neighbor buckets
                d.put(m, (long)nums[i]);
                if (i >= k) d.remove(getID(nums[i - k], w));
            }
            return false;
        }
    }



