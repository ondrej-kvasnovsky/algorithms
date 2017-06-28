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

Complexity is about O\(1/4\(n^2\)\) in optimistic case - when the array is partially sorted, this algorithm works perfectly In worst case, it is O\(1/2\(n^2\)\) - when the values in reversed order.

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

### Shell Sort

O\(n^\(3/2\).

```
class ShellSortArray {

    static void main(String[] args) {
        int[] array = [1, 5, 7, 3, 9, 1, -2]
        println array
        sort(array)
        println array
    }

    static void sort(int[] a) {
        int N = a.length;
        int h = 1;
        while (h < N / 3) h = 3 * h + 1; // 1, 4, 13, 40, 121, 364, ...

        while (h >= 1) {  // h-sort the array.
            for (int i = h; i < N; i++) {
                for (int j = i; j >= h && a[j] < a[j - h]; j -= h) {
                    int temp = a[j]
                    a[j] = a[j - h];
                    a[j - h] = temp;

                }
            }
            h = h / 3;
        }
    }
}
```

### Example: shuffle cards randomly

First idea: Generate random numbers and assign them to cards. Then sort the array. 

Knuth shuffle: iterate through the cards and generate random number that is between 0 and **i** \(**i** is current index\).

### Convex Hull

![](/assets/Screen Shot 2017-06-27 at 7.17.24 PM.png)

![](/assets/Screen Shot 2017-06-27 at 7.22.23 PM.png)

