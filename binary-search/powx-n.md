# Pow\(x, n\)

Implement[pow\(_x_,_n_\)](http://www.cplusplus.com/reference/valarray/pow/), which calculates _x_raised to the power_n_\(xn\).

**Example 1:**

```
Input: 2.00000, 10
Output: 1024.00000
```

**Example 2:**

```
Input: 2.10000, 3
Output: 9.26100
```

**Example 3:**

```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

## Solution

Brute force solution. 

```
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        double ans = 1;
        for (long i = 0; i < N; i++)
            ans = ans * x;
        return ans;
    }
}
```

**Intuition**

Assuming we have got the result ofxnx​n​​, how can we getx2∗nx​2∗n​​? Obviously we do not need to multiply`x`for another`n`times. Using the formula\(xn\)=x2∗n\(x​n​​\)​2​​=x​2∗n​​, we can getx2∗nx​2∗n​​at the cost of only one computation. Using this optimization, we can reduce the time complexity of our algorithm.

**Algorithm**

Assume we have got the result ofxn/2x​n/2​​, and now we want to get the result ofxnx​n​​. Let`A`be result ofxn/2x​n/2​​, we can talk aboutxnx​n​​based on the parity of`n`respectively. If`n`is even, we can use the formula\(xn\)=x2∗n\(x​n​​\)​2​​=x​2∗n​​to getxn=A∗Ax​n​​=A∗A. If`n`is odd, thenA∗A=xn−1A∗A=x​n−1​​. Intuitively, We need to multiply anotherxxto the result, soxn=A∗A∗xx​n​​=A∗A∗x. This approach can be easily implemented using recursion. We call this method "**Fast Power**", because we only need at mostO\(log\(n\)\)O\(log\(n\)\)computations to getxnx​n​​.

```
class Solution {
    private double fastPow(double x, long n) {
        if (n == 0) {
            return 1.0;
        }
        double half = fastPow(x, n / 2);
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
    public double myPow(double x, int n) {
        long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        return fastPow(x, N);
    }
}
```

Iterative version of previous algorithm. 

```
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        double ans = 1;
        double current_product = x;
        for (long i = N; i > 0; i /= 2) {
            if ((i % 2) == 1) {
                ans = ans * current_product;
            }
            current_product = current_product * current_product;
        }
        return ans;
    }
}
```



