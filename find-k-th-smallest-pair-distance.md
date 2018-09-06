# Find K-th Smallest Pair Distance

Given an integer array, return the k-th smallest **distance **among all the pairs. The distance of a pair \(A, B\) is defined as the absolute difference between A and B.

**Example 1:**

```
Input:
nums = [1,3,1]
k = 1
Output: 0 
Explanation:
Here are all the pairs:
(1,3) -> 2
(1,1) -> 0
(3,1) -> 2
Then the 1st smallest distance pair is (1,1), and its distance is 0.
```

**Note:**

1. `2 <= len(nums) <= 10000`.
2. `0 <= nums[i] < 1000000`.
3. `1 <= k <= len(nums) * (len(nums) - 1) / 2`.

## Solution

```
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
        Arrays.sort(nums);

        int lo = 0;
        int hi = nums[nums.length - 1] - nums[0]; // get the highest difference
        while (lo < hi) {
            int mi = (lo + hi) / 2; // go into middle
            int count = 0;
            int left = 0;
            for (int right = 0; right < nums.length; ++right) { // 
                while (nums[right] - nums[left] > mi)  {
                    left++;
                }
                count += right - left;
            }
            // count = number of pairs with distance <= mi
            if (count >= k) {
                hi = mi;
            } else {
                lo = mi + 1;
            }
        }
        return lo;
    }
}
```



