# Pascal's Triangle

Given a non-negative integer _numRows_, generate the first_numRows_of Pascal's triangle.

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)  
In Pascal's triangle, each number is the sum of the two numbers directly above it.

**Example:**

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## Solution

```
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<>();

        for (int i = 1; i <= numRows; i++) {
            Integer[] row = new Integer[i];
            row[0] = 1;
            row[row.length - 1] = 1;
            for (int j = 1; j < i - 1; j++) {
                List<Integer> integers = result.get(i - 2);
                int a = integers.get(j - 1);
                int b = integers.get(j);
                row[j] = a + b;
            }
            result.add(new ArrayList<>(Arrays.asList(row)));
        }

        return result;
    }
}
```



