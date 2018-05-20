# Single Number

Given a **non-empty** array of integers, every element appears _twice _except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```

Here are couple of solutions. 

```
class Solution {
    public int singleNumber(int[] nums) {
        // 0. add every number and remove it if found, the single number will remain in the set
        Set<Integer> set = new HashSet<>();
        for (int i : nums) {
            if (set.contains(i)) {
                set.remove(i);
            } else {
                set.add(i);
            }
        }
        return set.iterator().next();
        
        // 1. sort, if the following number is not equal to the current number, that number is the single
//         Arrays.sort(nums); // n log n
//         for (int i = 0; i < nums.length; i += 2) { // 0 2 4 // n / 2
//             if (i + 1 >= nums.length) { // 5 (0, 1, 2, 3, 4)
//                 return nums[i];
//             }
//             if (nums[i] != nums[i + 1]) {
//                 return nums[i];
//             }
//         }
//         return -1;
        
        // 2. the same as 1), just looping differently
//         if (nums.length == 1) {
//             return nums[0];
//         }
//         Arrays.sort(nums);
//         for (int i = 0, j = nums.length - 1; i < j; i += 2, j -= 2) {
//             if (nums[i] != nums[i + 1]) {
//                 return nums[i];
//             }
//             if (nums[j] != nums[j - 1]) {
//                 return nums[j];
//             }
//         }

//         return -1;
        
        // 4. first we add all numbers, then we sum them, the difference is the unique number (kind of over complicated)
//         Set<Integer> set = new HashSet<>();
//         for (int i = 0; i < nums.length; i++) {
//             set.add(nums[i]);
//         }

//         int s1 = 0;
//         Iterator<Integer> iterator = set.iterator();
//         while(iterator.hasNext()) {
//             s1 += iterator.next();
//         }

//         int s2 = 0;
//         for(int n : nums) {
//             s2 += n;
//         }

//         return 2 * s1 - s2;
        
        // 5. the same as 4, just fewer steps
//         Set<Integer> set = new HashSet<>();
//         int s2 = 0;
//         for (int i = 0; i < nums.length; i++) {
//             int num = nums[i];
//             set.add(num);
//             s2 += num;
//         }

//         int s1 = 0;
//         Iterator<Integer> iterator = set.iterator();
//         while(iterator.hasNext()) {
//             s1 += iterator.next();
//         }

//         return 2 * s1 - s2;
    }
}
```



