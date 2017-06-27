# Elementary Sorts

### Selection Sort

O\(\(n^2\)/2\)

```
class SortArray {

    static void main(String[] args) {
        int[] array = [1, 5, 7, 3, 9, 1, -2]
        println array
        sort(array)
        println array
    }

    static void sort(int[] array) {
        int min
        int temp
        for (int i = 0; i < array.length; i++) {
            min = i
            for (int j = i + 1; j < array.length; j++) {
                if (array[j] < array[min]) {
                    min = j
                }
            }
            temp = array[i]
            array[i] = array[min];
            array[min] = temp;
        }
    }
}
```

### Insertion Sort



