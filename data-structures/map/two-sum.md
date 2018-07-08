# Two Sum

Given an array of integers, return **indices **of the two numbers such that they add up to a specific target.

You may assume that each input would have \_**exactly **\_one solution, and you may not use the \_same \_element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solution

Here is a solution that is using hash map.

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> temp = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int number = nums[i];
            int difference = target - number; 
            if (temp.containsKey(difference)) {
                return new int[] { temp.get(difference), i };
            }
            temp.put(number, i);
        }

        return null;
    }
}
```

Two pass hash map. 

```
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

Brute force approach. 

```
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```



