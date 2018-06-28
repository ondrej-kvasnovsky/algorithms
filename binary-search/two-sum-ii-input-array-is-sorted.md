# Two Sum II - Input array is sorted

Given an array of integers that is already _**sorted in ascending order**_, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

* Your returned answers \(both index1 and index2\) are not zero-based.
* You may assume that each input would have _exactly _one solution and you may not use the _same _element twice. 

**Example:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

## Solution

Using binary search. 

```
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        // use binary search
        int start = 0;
        int end = numbers.length - 1;
        while (start < end) {
            int sum = numbers[start] + numbers[end];
            if (sum == target) {
                return new int[]{ start + 1, end + 1 };
            }
            if (sum > target) {
                end--;
            } else {
                start++;
            }
        }
        
        return new int[]{ -1, -1 };
    }
}
```



