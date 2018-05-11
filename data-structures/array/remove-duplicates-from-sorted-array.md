# Remove Duplicates from Sorted Array

Given a sorted array_nums_, remove the duplicates[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)such that each element appear only_once_and return the new length.

Do not allocate extra space for another array, you must do this by**modifying the input array**[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)with O\(1\) extra memory.

**Example 1:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by**reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

Here is a solution. 

```
class Solution {
    public int removeDuplicates(int[] nums) {
        // create current index that will a running number, increase always when another number is found - count = 0
        // iterate through the array and keep the value in current value variable (1)
        // compare if the nums[i] value is bigger than the current value
        // if yes -> write position on count, increment count++ 
        // else continue reading
        int count = 0;
        int latestValue = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            if (latestValue < num) {
                nums[count] = num;
                latestValue = num;
                count++;
            }
        }
        return count;
    }
}
```



