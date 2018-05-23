# Valid Sudoku

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9`without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9`3x3`sub-boxes of the grid must contain the digits `1-9` without repetition.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)  
A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character`'.'`.

**Example 1:**

```
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```

**Example 2:**

```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Note:**

* A Sudoku board \(partially filled\) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.
* The given board contain only digits`1-9`and the character`'.'`.
* The given board size is always`9x9`.

Here is a solution. First we check rows, then columns and then squares. This is some kind of hard core solution. 

```
class Solution {
    public boolean isValidSudoku(char[][] board) {

        for (int i = 0; i < board.length; i++) {
            // check rows
            char[] row = board[i];
            System.out.println(Arrays.toString(row));
            if (containsDuplicate(row)) {
                return false;
            }
            // columns
            char[] column = new char[] {
                board[0][i],
                board[1][i],
                board[2][i],
                board[3][i],
                board[4][i],
                board[5][i], 
                board[6][i], 
                board[7][i], 
                board[8][i]
            };
            if (containsDuplicate(column)) {
                return false;
            }
        }

        // squares
        for (int i = 0; i < board.length; i = i + 3) {
            for (int j = 0; j < board.length; j = j + 3) {
                char[] square = new char[] {
                    board[i][j + 0],
                    board[i][j + 1],
                    board[i][j + 2],
                    board[i + 1][j + 0],
                    board[i + 1][j + 1],
                    board[i + 1][j + 2], 
                    board[i + 2][j + 0], 
                    board[i + 2][j + 1], 
                    board[i + 2][j + 2]
                };
                if (containsDuplicate(square)) {
                    return false;
                }
            }
        }
        return true;
    }

    private boolean containsDuplicate(char[] values) {
        Set<Character> set = new HashSet<>();
        for (char value : values) {
            if (value == '.') continue;
            if (set.contains(value)) {
                return true;
            }
            set.add(value);
        }
        return false;
    }
}
```

Other solution is to use hash map and check what element we have seen for each case \(row, column and square\). We would like to generate unique string for each item on the row, in the column and in the square. 

```
5 in row 0
5 in column 0
5 in square 0-0
3 in row 0
3 in column 1
3 in square 0-0
7 in row 0
7 in column 4
7 in square 0-1
6 in row 1
6 in column 0
6 in square 0-0
1 in row 1
1 in column 3
1 in square 0-1
9 in row 1
9 in column 4
9 in square 0-1
5 in row 1
5 in column 5
5 in square 0-1
9 in row 2
9 in column 1
9 in square 0-0
8 in row 2
8 in column 2
8 in square 0-0
6 in row 2
6 in column 7
6 in square 0-2
8 in row 3
8 in column 0
8 in square 1-0
6 in row 3
6 in column 4
6 in square 1-1
3 in row 3
3 in column 8
3 in square 1-2
4 in row 4
4 in column 0
4 in square 1-0
8 in row 4
8 in column 3
8 in square 1-1
3 in row 4
3 in column 5
3 in square 1-1
1 in row 4
1 in column 8
1 in square 1-2
7 in row 5
7 in column 0
7 in square 1-0
2 in row 5
2 in column 4
2 in square 1-1
6 in row 5
6 in column 8
6 in square 1-2
6 in row 6
6 in column 1
6 in square 2-0
2 in row 6
2 in column 6
2 in square 2-2
8 in row 6
8 in column 7
8 in square 2-2
4 in row 7
4 in column 3
4 in square 2-1
1 in row 7
1 in column 4
1 in square 2-1
9 in row 7
9 in column 5
9 in square 2-1
5 in row 7
5 in column 8
5 in square 2-2
8 in row 8
8 in column 4
8 in square 2-1
7 in row 8
7 in column 7
7 in square 2-2
9 in row 8
9 in column 8
9 in square 2-2
```

Here is the code that will do it.

```
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Set<String> set = new HashSet<>();
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board.length; j++) {
                char val = board[i][j];
                if (val == '.') continue;
                String rowKey = val + " in row " + i;
                String columnKey = val + " in column " + j;
                String squareKey = val + " in square " + i/3 + "-" + j/3;
                System.out.println(rowKey);
                System.out.println(columnKey);
                System.out.println(squareKey);
                if (set.contains(rowKey) || set.contains(columnKey) || set.contains(squareKey)) {
                    return false;
                } else {
                    set.add(rowKey);
                    set.add(columnKey);
                    set.add(squareKey);
                }
            }
        }
        
        return true;
    }
}
```



