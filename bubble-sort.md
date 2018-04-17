# Bubble Sort

Complexity: `O(n^2)`. 

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



