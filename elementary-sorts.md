# Elementary Sorts

### Selection Sort

O\(1/2\(n^2\)\)

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

O\(1/4\(n^2\)\)

```
class InsertionSortArray {

    static void main(String[] args) {
        int[] array = [1, 5, 7, 3, 9, 1, -2]
        println array
        sort(array)
        println array
    }

    static void sort(int[] array) {
        for (int i = 0; i < array.length; i++) {
            for (int j = i; j > 0; j--) {
                if (array[j] < array[j -1]) {
                    int temp = array[j]
                    array[j] = array[j - 1]
                    array[j - 1] = temp;
                } else {
                    break
                }
            }
        }
    }
}
```



