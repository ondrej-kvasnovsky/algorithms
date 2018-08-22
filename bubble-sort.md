# Bubble Sort

Complexity: `O(n^2)`.

Very basic implementation. 

```
public class BubbleSort2 {

    public static void main(String[] args) {
        int[] array = {5, 4, 3, 100, 1};

        for (int i = 0; i < array.length; i++) {
            for (int j = 0; j < array.length; j++) {
                if (array[i] < array[j]) {
                    int temp = array[i];
                    array[i] = array[j];
                    array[j] = temp;
                }
            }
        }

        System.out.println(Arrays.toString(array));
    }
}
```

Another implementation where we limit ending boundaries.

```
import java.util.Arrays;

public class Demo {

    public static void main(String... args) {
        int[] array = new int[]{3, 2, 4, 5, 1};
        // 0, 1, 2, 3, 4
        // -------------
        // 2, 3, 4, 1, 5
        // 2, 3, 1, 4, 5
        // 2, 1, 3, 4, 5
        // 1, 2, 3, 4, 5

        for (int i = 0; i < array.length - 1; i++) {
            for (int j = 0; j < array.length - i - 1; j++) {
                int first = array[j];
                int second = array[j + 1];
                if (first > second) {
                    // swap if first is bigger than second
                    array[j] = second;
                    array[j + 1] = first;
                }
                System.out.println(Arrays.toString(array));
            }
        }

        System.out.println(Arrays.toString(array));
    }
}
```

Once I was asked to implement whatever sorting algorithm \(on a phone interview\). I came up with this algorithm to sort an array. It is some kind of version of bubble sort, I guess. I am not sure why I did that, I think pressure and stress really worked out.

```
package algorithms.doordash;

import java.util.Arrays;

public class Phone1 {

    public static void main(String[] args) {
        int[] array = {41, 3, 2, 21, 3, 21, 1, -100, 0, 1000};
        sort(array);
        System.out.println(Arrays.toString(array));
    }

    private static void sort(int[] array) {
        int length = array.length - 1;
        int minVal = Integer.MIN_VALUE;
        for (int i = 0; i < length; ) {
            int index1 = i;
            int index2 = i + 1;
            while (index2 < length + 1) {
                minVal = Math.min(array[index1], array[index2]);
                if (array[index1] > array[index2]) {
                    swap(index1, index2, array);
                }
                index2++;
            }
            if (minVal <= array[index1]) {
                i++;
            }
        }
    }

    public static void swap(int index1, int index2, int[] array) {
        int temp = array[index2];
        array[index2] = array[index1];
        array[index1] = temp;
    }
}
```



