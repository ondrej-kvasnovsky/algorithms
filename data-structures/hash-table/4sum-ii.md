# 4Sum II

Given four lists A, B, C, D of integer values, compute how many tuples`(i, j, k, l)`there are such that`A[i] + B[j] + C[k] + D[l]`is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228to 228- 1 and the result is guaranteed to be at most 231- 1.

**Example:**

```
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

Here is a solution. 

```
class Solution {
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        // create all sums from A and B and put their negative values into map (key is number and value is number of occurances)
        // then create all sums from C and B and try to find them int the set we made, if found, we got 0 
        // and we increment the value
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < B.length; j++) {
                int negativeSum = -(A[i] + B[j]);
                map.put(negativeSum, map.getOrDefault(negativeSum, 0) + 1);
            }
        }

        int count = 0;
        for (int i = 0; i < C.length; i++) {
            for (int j = 0; j < D.length; j++) {
                int sum = C[i] + D[j];
                if (map.containsKey(sum)) {
                    count += map.get(sum);
                }
            }
        }
        return count;
    }
}
```



