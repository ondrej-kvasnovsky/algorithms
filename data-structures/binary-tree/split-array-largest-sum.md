# Split Array Largest Sum

Given an array which consists of non-negative integers and an integerm, you can split the array intomnon-empty continuous subarrays. Write an algorithm to minimize the largest sum among thesemsubarrays.

**Note:**  
Ifnis the length of array, assume the following constraints are satisfied:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min\(50,n\)

**Examples:**

```
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

## Solution

#### Approach \#1 Brute Force \[Time Limit Exceeded\] {#approach-1-brute-force-time-limit-exceeded}

**Intuition**

Check all possible splitting plans to find the minimum largest value for subarrays.

**Algorithm**

We can use depth-first search to generate all possible splitting plan. For each element in the array, we can choose to append it to the previous subarray or start a new subarray starting with that element \(if the number of subarrays does not exceed`m`\). The sum of the current subarray can be updated at the same time.

**Complexity Analysis**

* Time complexity :O\(nm\)O\(n​m​​\). To split`n`elements into`m`parts, we can have\(n−1m−1\)\(​m−1​n−1​​\)different solutions. This is equivalent tonmn​m​​.

* Space complexity :O\(n\)O\(n\). We only need the space to store the array.

```
class Solution {
    private int ans;
    private int n, m;
    private void dfs(int[] nums, int i, int cntSubarrays, int curSum, int curMax) {
        if (i == n && cntSubarrays == m) {
            ans = Math.min(ans, curMax);
            return;
        }
        if (i == n) {
            return;
        }
        if (i > 0) {
            dfs(nums, i + 1, cntSubarrays, curSum + nums[i], Math.max(curMax, curSum + nums[i]));
        }
        if (cntSubarrays < m) {
            dfs(nums, i + 1, cntSubarrays + 1, nums[i], Math.max(curMax, nums[i]));
        }
    }
    public int splitArray(int[] nums, int M) {
        ans = Integer.MAX_VALUE;
        n = nums.length;
        m = M;
        dfs(nums, 0, 0, 0, 0);
        return ans;
    }
}
```

#### Approach \#2 Dynamic Programming \[Accepted\] {#approach-2-dynamic-programming-accepted}

**Intuition**

The problem satisfies the non-aftereffect property. We can try to use dynamic programming to solve it.

The non-aftereffect property means, once the state of a certain stage is determined, it is not affected by the state in the future. In this problem, if we get the largest subarray sum for splitting`nums[0..i]`into`j`parts, this value will not be affected by how we split the remaining part of`nums`.

To know more about non-aftereffect property, this link may be helpful :[http://www.programering.com/a/MDOzUzMwATM.html](http://www.programering.com/a/MDOzUzMwATM.html)

**Algorithm**

Let's define`f[i][j]`to be the minimum largest subarray sum for splitting`nums[0..i]`into`j`parts.

Consider the`j`th subarray. We can split the array from a smaller index`k`to`i`to form it. Thus`f[i][j]`can be derived from`max(f[k][j - 1], nums[k + 1] + ... + nums[i])`. For all valid index`k`,`f[i][j]`should choose the minimum value of the above formula.

The final answer should be`f[n][m]`, where`n`is the size of the array.

For corner situations, all the invalid`f[i][j]`should be assigned with`INFINITY`, and`f[0][0]`should be initialized with`0`.

**Complexity Analysis**

* Time complexity :O\(n2∗m\)O\(n​2​​∗m\). The total number of states isO\(n∗m\)O\(n∗m\). To compute each state`f[i][j]`, we need to go through the whole array to find the optimum`k`. This requires anotherO\(n\)O\(n\)loop. So the total time complexity isO\(n2∗m\)O\(n​2​​∗m\).

* Space complexity :O\(n∗m\)O\(n∗m\). The space complexity is equivalent to the number of states, which isO\(n∗m\)O\(n∗m\).

```

class Solution {
    public int splitArray(int[] nums, int m) {
        int n = nums.length;
        int[][] f = new int[n + 1][m + 1];
        int[] sub = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                f[i][j] = Integer.MAX_VALUE;
            }
        }
        for (int i = 0; i < n; i++) {
            sub[i + 1] = sub[i] + nums[i];
        }
        f[0][0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                for (int k = 0; k < i; k++) {
                    f[i][j] = Math.min(f[i][j], Math.max(f[k][j - 1], sub[i] - sub[k]));
                }
            }
        }
        return f[n][m];        
    }
}
```

#### Approach \#3 Binary Search + Greedy \[Accepted\] {#approach-3-binary-search-greedy-accepted}

**Intuition**

We can easily find a property for the answer:

> If we can find a splitting method that ensures the maximum largest subarray sum will not exceed a value`x`, then we can also find a splitting method that ensures the maximum largest subarray sum will not exceed any value`y`that is greater than`x`.

Lets define this property as`F(x)`for the value`x`.`F(x)`is true means we can find a splitting method that ensures the maximum largest subarray sum will not exceed`x`.

From the discussion above, we can find out that for`x`ranging from`-INFINITY`to`INFINITY`,`F(x)`will start with false, then from a specific value`x0`,`F(x)`will turn to true and stay true forever.

Obviously, the specific value`x0`is our answer.

**Algorithm**

We can use Binary search to find the value`x0`. Keeping a value`mid = (left + right) / 2`. If`F(mid)`is false, then we will search the range`[mid + 1, right]`; If`F(mid)`is true, then we will search`[left, mid - 1]`.

For a given`x`, we can get the answer of`F(x)`using a greedy approach. Using an accumulator`sum`to store the sum of the current processing subarray and a counter`cnt`to count the number of existing subarrays. We will process the elements in the array one by one. For each element`num`, if`sum + num <= x`, it means we can add`num`to the current subarray without exceeding the limit. Otherwise, we need to make a cut here, start a new subarray with the current element`num`. This leads to an increment in the number of subarrays.

After we have finished the whole process, we need to compare the value`cnt`to the size limit of subarrays`m`. If`cnt <= m`, it means we can find a splitting method that ensures the maximum largest subarray sum will not exceed`x`. Otherwise,`F(x)`should be false.

**Complexity Analysis**

* Time complexity :O\(n∗log\(sumofarray\)\)O\(n∗log\(sumofarray\)\). The binary search costsO\(log\(sumofarray\)\)O\(log\(sumofarray\)\), where`sum of array`is the sum of elements in`nums`. For each computation of`F(x)`, the time complexity isO\(n\)O\(n\)since we only need to go through the whole array.

* Space complexity :O\(n\)O\(n\). Same as the Brute Force approach. We only need the space to store the array.

```
class Solution {
    public int splitArray(int[] nums, int m) {
        long l = 0;
        long r = 0;        
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            r += nums[i];
            if (l < nums[i]) {
                l = nums[i];
            }
        }
        long ans = r;
        while (l <= r) {
            long mid = (l + r) >> 1;
            long sum = 0;
            int cnt = 1;
            for (int i = 0; i < n; i++) {
                if (sum + nums[i] > mid) {
                    cnt ++;
                    sum = nums[i];
                } else {
                    sum += nums[i];
                }
            }
            if (cnt <= m) {
                ans = Math.min(ans, mid);
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return (int)ans;      
    }
}
```



