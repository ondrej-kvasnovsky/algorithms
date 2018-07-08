# 3Sum

Given an array`nums`of _n _integers, are there elements _a_, _b_, _c _in `nums` such that _a_+_b_+_c_= 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Solution

O\(n pow 3\) solution is as follows, but it does not prevent duplicates. 

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        
        for (int i = 0; i < nums.length - 2; i++) {
            for (int j = i + 1; j < nums.length - 1; j++) {
                for (int k = j + 1; k < nums.length; k++) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        List<Integer> found = new ArrayList<>();
                        found.add(nums[i]);
                        found.add(nums[j]);
                        found.add(nums[k]);
                        result.add(found);
                    }
                }
            }
        }
        
        return result;
    }
}
```



