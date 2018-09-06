* [ ] # Diagonal Traverse

Given a matrix of M x N elements \(M rows, N columns\), return all elements of the matrix in diagonal order as shown in the below image.

**Example:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output:  [1,2,4,7,5,3,6,8,9]
```

## Solution

Here is a non-optimized solution \(from code readability point of view\).

```
class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        int rows = matrix.length;
        if (rows == 0) {
            return new int[0];
        }
        int columns = matrix[0].length;
        int index = 0;
        int row = 0;
        int column = 0;
        int[] result = new int[rows * columns];
        boolean goingUp = true;
        while (row < rows && column < columns) {
            System.out.println(row + " " + column);
            result[index++] = matrix[row][column];
            System.out.println(Arrays.toString(result));
            if (goingUp) {
                boolean isLastColumn = column == columns - 1;
                if (row == 0 || isLastColumn) {
                    goingUp = false;
                    if (isLastColumn) {
                        row++;
                    } else {
                        column++;
                    }
                } else {
                    row--;
                    column++;
                }
            } else {
                boolean isLastRow = row == rows - 1;
                if (column == 0 || isLastRow) {
                    goingUp = true;
                    if (isLastRow) {
                        column++;
                    } else {
                        row++;                        
                    }
                } else {
                    row++;
                    column--;
                }
            }
        }
        return result;
    }
}
```

When we simplify the algorighm we can get into something like this. Boolean goingUp variable is replaced by % 2 because if the modulo of a number is 0, we are going up.

| row | column | direction |
| :--- | :--- | :--- |
| 0 | 0 | up |
| 1 | 0 | down |
| 0 | 2 | up |
| 2 | 1 | down |

Then we can simplify the code \(to make it less readable\).

```
    public int[] findDiagonalOrder(int[][] matrix) {
        if (matrix.length == 0) return new int[0];
        int r = 0;
        int c = 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int[] arr = new int[m * n];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = matrix[r][c];
            if ((r + c) % 2 == 0) { // moving up
                if (c == n - 1) { r++; }
                else if (r == 0) { c++; }
                else { r--; c++; }
            } else { // moving down
                if (r == m - 1) { c++; }
                else if (c == 0) { r++; }
                else { r++; c--; }
            }
        }
        return arr;
    }
```



