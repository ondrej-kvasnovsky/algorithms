# Shuffle an Array

Shuffle a set of numbers without duplicates.

**Example:**

```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```

## Solution

```
class Solution {

    int[] original;
    Random r = new Random();
    
    public Solution(int[] nums) {
        this.original = nums;
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return original;
    }
    
    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        int[] shuffled = original.clone();
        for (int i = 0; i < shuffled.length; i++) {
            int position = r.nextInt(shuffled.length);
            int temp = shuffled[position];
            shuffled[position] = shuffled[i];
            shuffled[i] = temp;
        }
        return shuffled;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```



