# Matrix

[Matrix](https://en.wikipedia.org/wiki/Matrix_%28mathematics%29) is also called 2-dimensional array. 

```
class NaiveMatrix {

    private Integer[][] values;

    public NaiveMatrix(int n, int m) {
        this.values = new Integer[n][m];
        for (int row = 0; row < values.length; row++) {
            for (int column = 0; column < values[row].length; column++) {
                values[row][column] = 0;
            }
        }
    }

    public void set(int row, int column, Integer value) {
        values[row][column] = value;
    }

    public Integer get(int i, int j) {
        return values[i][j];
    }

    public String toString() {
        StringBuilder result = new StringBuilder();
        for (Integer[] row : values) {
            for (Integer value : row) {
                result.append(value);
                result.append(" ");
            }
            result.append("\n");
        }
        return result.toString();
    }
}
```

Lets try to use this matrix implementation. 

```
public class MatrixDemo {

    public static void main(String... args) {
        NaiveMatrix matrix = new NaiveMatrix(2, 3);
        matrix.set(0, 0, 5);
        matrix.set(0, 1, 5);
        matrix.set(0, 2, 5);
        System.out.println(matrix);
    }
}
```

The code above prints out the following. 

```
5 5 5 
0 0 0 
```

### Matrix operations

There are many operations that are described in [linear algebra](https://www.khanacademy.org/math/algebra-home/alg-matrices). We are going to implement couple of these. We are going to enhance `NaiveMatrix` class with more operations.

#### Addition

Adds to matrices together, summing each element on that position.

```
    public NaiveMatrix add(NaiveMatrix matrix) {
        NaiveMatrix sum = new NaiveMatrix(values.length, values[0].length);
        for (int row = 0; row < values.length; row++) {
            for (int column = 0; column < values[row].length; column++) {
                sum.values[row][column] = values[row][column] + matrix.values[row][column];
            }
        }
        return sum;
    }
```

Then we can create two matrices and sum them together. 

```
public class MatrixDemo {

    public static void main(String... args) {
        NaiveMatrix matrix = new NaiveMatrix(2, 3);
        matrix.set(0, 0, 5);
        matrix.set(0, 1, 5);
        matrix.set(0, 2, 5);
        System.out.println(matrix);

        NaiveMatrix matrix2 = new NaiveMatrix(2, 3);
        matrix2.set(0, 0, 1);
        NaiveMatrix sum = matrix.add(matrix2);
        System.out.println(sum);
    }
}
```

Here is how the output would look like. 

```
5 5 5 
0 0 0 

6 5 5 
0 0 0 
```

#### 































