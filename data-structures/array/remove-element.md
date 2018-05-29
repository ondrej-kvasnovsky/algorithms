# Remove Element

Given an array_nums_and a value_val_, remove all instances of that value[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)and return the new length.

Do not allocate extra space for another array, you must do this by**modifying the input array**[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)with O\(1\) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by**reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

## Solution

```
class Solution {
    public int removeElement(int[] nums, int val) {
        // idea 1: nums=[1, 1, 2], val=1 => i=0, found, find other value and swap, increment counter
        // init new variable currentIndex = 0
        // nums: 1, 1, 2 | val: 1 => lentgh: 1 | nums: [2, -, -] 
        // iterate through array, i => num = nums[i]
        // if num == val => swap it with the next value which is not val 
        //      -> while loop from i to the next position, then currentIndex++, increase i to index from the while loop
        // else continue... 
        int counter = 0;
        
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            if (num == val) {
                // find other value and swap
                // i=2, j=6 j=5
                for (int j = nums.length - 1; j >= i; j--) {
                    if (nums[j] != val) {
                        swap(nums, i, j);
                        counter++;
                        break;
                    }
                }
            } else {
                counter++;
            }
        }
        return counter;
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

## Solution using Two pointers

```
class Solution {
    public int removeElement(int[] nums, int val) {
        int counter = 0;
        // count every time we had to switch value (so when two values were not equal)
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[counter] = nums[i];
                counter++;
            }
        }
        
        return counter;
    }
}
```



