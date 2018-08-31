# Insertion Sort

Insertion sort is moving smaller values to the left of the array, while it is still smaller then the value on left.

```
package sorting;

import java.util.Arrays;

public class InsertionSort {

    public static void main(String[] args) {
        int[] array = {5, 4, 3, 2, 1};
        insertionSort(array);
    }

    public static void insertionSort(int[] array) {
        int j;
        for (int i = 1; i < array.length; i++) {
            j = i;
            while ((j > 0) && (array[j] < array[j - 1])) {
                swap(array, j,j - 1);
                j = j - 1;
                System.out.println(Arrays.toString(array));
            }
        }
    }

    public static void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
```

Here is the output to illustrate what happend.

```
[5, 4, 3, 2, 1]
[4, 5, 3, 2, 1]
[4, 3, 5, 2, 1]
[3, 4, 5, 2, 1]
[3, 4, 2, 5, 1]
[3, 2, 4, 5, 1]
[2, 3, 4, 5, 1]
[2, 3, 4, 1, 5]
[2, 3, 1, 4, 5]
[2, 1, 3, 4, 5]
[1, 2, 3, 4, 5]
```



