# Move Zeroes

Given an array`nums`, write a function to move all`0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place **without making a copy of the array.
2. Minimize the total number of operations.

## Solution

I was thinking about this solution but it does not keep order and is also very efficient.

```
class Solution {
    public void moveZeroes(int[] nums) {
        // use two pointers strategy
        // iterate through array
        // create index to last position in array (this will indicate where to put 0 - or at least candidate where to put 0)
        // if 0 is found -> move all left to right (if zero is found) - why not to go from right then?

        // [true, false, true, false, false]
        int start = 0;
        int end = nums.length - 1;

        while (start < end) {
            int num1 = nums[start];
            if (num1 == 0) {
                int num2 = nums[end];
                while (num2 == 0 && end > start) {
                    end--;
                    num2 = nums[end];
                }
                // swap values
                if (num2 != 0) {
                    System.out.println(nums[start] + ":" + nums[end]);
                    int temp = nums[start];
                    nums[start] = num2;
                    nums[end] = temp;    
                }
            }
            start++;
        }
    }
}
```

Other solution would be to have two pointers \(starting at the begging\). First index is current index that iterates through array. The second index is the index of the last non zero value. When we find 0, we can swap the values.

```
class Solution {
    public void moveZeroes(int[] nums) {
        int current = 0;
        int lastNotZeroIndex = 0;

        while (current < nums.length) {
            int num = nums[current];
            if (num != 0) {
                nums[current] = nums[lastNotZeroIndex];
                nums[lastNotZeroIndex] = num;    
                lastNotZeroIndex++;
            }
            current++;
            System.out.println("current: " + current + ", lastNotZeroIndex: " + lastNotZeroIndex);
            System.out.println(Arrays.toString(nums));
        }
    }
}
```

For this input, `[0,1,0,3,12]`. We get the following intermediate results.

```
current: 1, lastNotZeroIndex:0
[0, 1, 0, 3, 12]

current: 2, lastNotZeroIndex:1
[1, 0, 0, 3, 12]

current: 3, lastNotZeroIndex:1
[1, 0, 0, 3, 12]

current: 4, lastNotZeroIndex:2
[1, 3, 0, 0, 12]

current: 5, lastNotZeroIndex:3
[1, 3, 12, 0, 0]
```



