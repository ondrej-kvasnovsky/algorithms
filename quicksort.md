# Quick Sort

[Here](https://www.youtube.com/watch?v=ZHVk2blR45Q) is a very good explanation of quick sort by Rob Edwards from SDSU.

Is O\(n log n\) complexity. Is not stable but can be done in-place. In worst case, it is O\(n^2\).

## Solution

Here is an implementation, similar to the one from the video.

```
package sorting;

import java.util.Arrays;

public class QuickSortRobEdwards {

    public static void main(String[] args) {
        int[] array = {6, 5, 4, 3, 2, 1};
        sort(array);
        System.out.println(Arrays.toString(array));
    }

    public static void sort(int[] array) {
        quicksort(array, 0, array.length - 1);
    }

    public static void quicksort(int[] array, int from, int to) {
        if (from >= to) return; // single element list is already sorted

        int pivotPointValue = array[to];
        int firstNumberThatIsLargeThanPivotPoint = from;
        for (int i = from; i < to; i++) {
            if (array[i] < pivotPointValue) {
                swap(array, i, firstNumberThatIsLargeThanPivotPoint);
                firstNumberThatIsLargeThanPivotPoint++;
            }
        }
        swap(array, firstNumberThatIsLargeThanPivotPoint, to);
        quicksort(array, from, firstNumberThatIsLargeThanPivotPoint - 1);
        quicksort(array, firstNumberThatIsLargeThanPivotPoint + 1, to);
    }

    public static void swap(int[] array, int from, int to) {
        int temp = array[from];
        array[from] = array[to];
        array[to] = temp;
    }
}
```



