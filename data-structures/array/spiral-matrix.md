# Spiral Matrix

Given a matrix of_m_x_n_elements \(_m_rows,_n_columns\), return all elements of the matrix in spiral order.

**Example 1:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

```
Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## Solution

The idea is to read outer squares or rectangles and then move the sides to the middle. 

```
class Solution {
    
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        if (matrix.length == 0) {
            return result;
        }
        int firstRow = 0;
        int lastRow = matrix.length - 1;
        int leftColumn = 0; 
        int rightColumn = matrix[0].length - 1;
        
        while (firstRow <= lastRow && leftColumn <= rightColumn) {
            // read first row
            for (int i = leftColumn; i <= rightColumn; i++) {
                result.add(matrix[firstRow][i]);
            }
            
            // read right column
            for (int i = firstRow + 1; i <= lastRow; i++) {
                result.add(matrix[i][rightColumn]);
            }
            // to avoid duplicates (reading it backwards)
            if (firstRow < lastRow && leftColumn < rightColumn) {
                // read last row
                for (int i = rightColumn - 1; i >= leftColumn; i--) {
                    result.add(matrix[lastRow][i]);
                }

                // read left column
                for (int i = lastRow - 1; i > firstRow; i--) {
                    result.add(matrix[i][leftColumn]);
                }
            }
            
            firstRow++; // move first row down
            rightColumn--; // move right column to left
            lastRow--; // move last row up
            leftColumn++; // move left column to right
            
        }
        
        return result;
    }
}



```



