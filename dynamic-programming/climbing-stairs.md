# Climbing Stairs

You are climbing a stair case. It takes _n _steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note: **Given _n _will be a positive integer.

**Example 1:**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## Solution

Brute force with recursion. O\(2^n​\)

```
public class Solution {
    public int climbStairs(int n) {
        return climb_Stairs(0, n);
    }
    public int climb_Stairs(int i, int n) {
        if (i > n) {
            return 0;
        }
        if (i == n) {
            return 1;
        }
        return climb_Stairs(i + 1, n) + climb_Stairs(i + 2, n);
    }
}
```

Brute force with memoization. O\(n\)

```
public class Solution {
    public int climbStairs(int n) {
        int memo[] = new int[n + 1];
        return climb_Stairs(0, n, memo);
    }

    public int climb_Stairs(int i, int n, int memo[]) {
        if (i > n) {
            return 0;
        }
        if (i == n) {
            return 1;
        }
        if (memo[i] > 0) {
            return memo[i];
        }
        memo[i] = climb_Stairs(i + 1, n, memo) + climb_Stairs(i + 2, n, memo);
        return memo[i];
    }
}
```

Dynamic programming. O\(n\).![](/assets/climginb-stairs.png)

Here is the code. 

```
import java.util.Arrays;

public class RotateImage {

    public static void main(String... args) {

        new Solution().climbStairs(10);
    }
}

class Solution {

    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            System.out.println(Arrays.toString(dp));
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

Here is the output. 

```
[0, 1, 2, 0, 0, 0, 0, 0, 0, 0, 0]
[0, 1, 2, 3, 0, 0, 0, 0, 0, 0, 0]
[0, 1, 2, 3, 5, 0, 0, 0, 0, 0, 0]
[0, 1, 2, 3, 5, 8, 0, 0, 0, 0, 0]
[0, 1, 2, 3, 5, 8, 13, 0, 0, 0, 0]
[0, 1, 2, 3, 5, 8, 13, 21, 0, 0, 0]
[0, 1, 2, 3, 5, 8, 13, 21, 34, 0, 0]
[0, 1, 2, 3, 5, 8, 13, 21, 34, 55, 0]
```

Using Fibonacci Number.

```
public class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int first = 1;
        int second = 2;
        for (int i = 3; i <= n; i++) {
            int third = first + second;
            first = second;
            second = third;
        }
        return second;
    }
}
```

Using Binets Method.

```
 public class Solution {
    public int climbStairs(int n) {
        int[][] q = {{1, 1}, {1, 0}};
        int[][] res = pow(q, n);
        return res[0][0];
    }
    public int[][] pow(int[][] a, int n) {
        int[][] ret = {{1, 0}, {0, 1}};
        while (n > 0) {
            if ((n & 1) == 1) {
                ret = multiply(ret, a);
            }
            n >>= 1;
            a = multiply(a, a);
        }
        return ret;
    }
    public int[][] multiply(int[][] a, int[][] b) {
        int[][] c = new int[2][2];
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 2; j++) {
                c[i][j] = a[i][0] * b[0][j] + a[i][1] * b[1][j];
            }
        }
        return c;
    }
}
```

Using Fibonacci Formula.

```
public class Solution {
    public int climbStairs(int n) {
        double sqrt5=Math.sqrt(5);
        double fibn=Math.pow((1+sqrt5)/2,n+1)-Math.pow((1-sqrt5)/2,n+1);
        return (int)(fibn/sqrt5);
    }
}
```



