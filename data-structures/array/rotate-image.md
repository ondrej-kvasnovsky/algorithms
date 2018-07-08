# Rotate Image

You are given an_n_x_n_2D matrix representing an image.

Rotate the image by 90 degrees \(clockwise\).

**Note:**

You have to rotate the image[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly.**DO NOT**allocate another 2D matrix and do the rotation.

**Example 1:**

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**Example 2:**

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

## Solution

Here is what kind of approach we want to do. We want to work with 4 pointers at a time. ![](/assets/rotate-image.png)

He is the algorithm. 

```
package algos;

import java.util.Arrays;

public class RotateImage {

    public static void main(String... args) {
        int[][] image = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}, {13, 14, 15, 16}};
        new Solution().rotate(image);
    }
}

class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int i = 0; i < n / 2; i++) {
            for (int j = i; j < n - i - 1; j++) {
                System.out.println("i: " + i + ", j: " + j);
                int temp = matrix[i][j]; // store first one, we 
                matrix[i][j] = matrix[n - j - 1][i];
                matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1];
                matrix[n - i - 1][n - j - 1] = matrix[j][n - i - 1];
                matrix[j][n - i - 1] = temp;
                System.out.println(Arrays.deepToString(matrix));
            }
        }
    }
}
```

Here is the output. 

```
i: 0, j: 0
[[13, 2, 3, 1], [5, 6, 7, 8], [9, 10, 11, 12], [16, 14, 15, 4]]
i: 0, j: 1
[[13, 9, 3, 1], [5, 6, 7, 2], [15, 10, 11, 12], [16, 14, 8, 4]]
i: 0, j: 2
[[13, 9, 5, 1], [14, 6, 7, 2], [15, 10, 11, 3], [16, 12, 8, 4]]
i: 1, j: 1
[[13, 9, 5, 1], [14, 10, 6, 2], [15, 11, 7, 3], [16, 12, 8, 4]]
```



