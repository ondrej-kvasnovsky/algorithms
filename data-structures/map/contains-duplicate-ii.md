# Contains Duplicate II

Given an array of integers and an integerk, find out whether there are two distinct indicesiandjin the array such that **nums\[i\] = nums\[j\] **and the **absolute **difference betweeniandjis at mostk.

**Example 1:**

```
Input: [1,2,3,1], k = 3
Output: true
```

**Example 2:**

```
Input: [1,0,1,1], k = 1
Output: true
```

**Example 3:**

```
Input: [1,2,1], k = 0
Output: false
```

Here is the output.

```
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        // create sliding window of k size
        // iterate through values
        // if value is found in the set, return true
        // store value in set
        // where key is index and value 
        // if set size is equal to K, remove first value
        if (k == 0) {
            return false;
        }
        
        Set<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
            if (set.size() > k) {
                // remove the oldest one
                set.remove(nums[i - k]);
            }
        }
        return false;
    }
}
```



