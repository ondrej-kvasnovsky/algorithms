# Diagonal Traverse

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



