# Max Area of Island

A non-recursive solution using stack.

```
class Solution {
    
    public int maxAreaOfIsland(int[][] grid) {
        Stack<Point> stack = new Stack<>();
        int max = 0;
        
        for (int row = 0; row < grid.length; row++) {
            for (int column = 0; column < grid[0].length; column++) {
                if (grid[row][column] == 1) {
                    grid[row][column] = 0;
                    stack.add(new Point(row, column));
                }
                if (!stack.isEmpty()) {
                    int currentMax = consumeStack(stack, grid);
                    max = Math.max(max, currentMax);
                }
            }
        }
        
        return max;
    }
    
    public int consumeStack(Stack<Point> stack, int[][] grid) {
        Integer max = 0;
        while(!stack.isEmpty()) {
            Point point = stack.pop();
            int row = point.row;
            int column = point.column;
            max++;
            if (row < grid.length - 1)
                if (grid[row + 1][column] == 1) {
                    grid[row + 1][column] = 0;
                    stack.add(new Point(row + 1, column));
                }
            if (row > 0)
                if (grid[row - 1][column] == 1) {
                    grid[row - 1][column] = 0;
                    stack.add(new Point(row - 1, column));
                }
            if (column > 0)
                if (grid[row][column - 1] == 1) {
                    grid[row][column - 1] = 0;
                    stack.add(new Point(row , column - 1));
                }
            if (column < grid[0].length - 1)
                if (grid[row][column + 1] == 1) {
                    grid[row][column + 1] = 0;
                    stack.add(new Point(row , column + 1));
                }
        }
        return max;
    }
}

class Point {
    int row;
    int column;
    Point(int row, int column) {
        this.row = row;
        this.column = column;
    }
}
```

Here is a recursive solution.

```
TODO:
```



