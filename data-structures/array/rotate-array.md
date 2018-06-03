# Rotate Array

Given an array, rotate the array to the right by_k_steps, where _k_ is non-negative.

**Example 1:**

```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**

```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

**Note:**

* Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
* Could you do it in-place with O\(1\) extra space?

## Solution

First idea was to create something what would just switch the halfs \(half is defined by K\). 

```
class Solution {
    public void rotate(int[] nums, int k) {
        if (k > nums.length) {
            return;
        }
        // read K elements of items from end into a new array, then read the rest into an array
        int[] arrray = new int[nums.length];
        int index = 0;
        for (int i = nums.length - k; i < nums.length; i++) {
            arrray[index++] = nums[i];
        }
        System.out.println(Arrays.toString(arrray));
        for (int i = 0; i < nums.length - k && index < nums.length; i++) {
            arrray[index++] = nums[i];
        }
        System.out.println(Arrays.toString(arrray));
        for (int i = 0; i < nums.length; i++) {
            nums[i] = arrray[i];
        }
    }
}
```

But it does not work for K which is bigger than length of nums. So it cannot rotate array couple of times. The issue is that it takes too much time to copy all values for each K. 

```
class Solution {
    public void rotate(int[] nums, int k) {
        int index = 0;
        while (k > 0) {
            int lastValue = nums[nums.length - 1];
            for (int i = nums.length - 2; i >= 0; i--) {
                nums[i + 1] = nums[i];
            }
            nums[0] = lastValue;
            k--;
        }
    }
}
```

So there needs to be faster solution. First reverse whole field. Then flip each side \(half is K\).

```
Original List                   : 1 2 3 4 5 6 7
After reversing all numbers     : 7 6 5 4 3 2 1
After reversing first k numbers : 5 6 7 4 3 2 1
After revering last n-k numbers : 5 6 7 1 2 3 4 --> Result
```

Here is the implementation. 

```
class Solution {
    public void rotate(int[] nums, int k) {
        swap(nums, 0, nums.length - 1);
        swap(nums, 0, k - 1);
        swap(nums, k, nums.length - 1);
    }
    
    private void swap(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```





