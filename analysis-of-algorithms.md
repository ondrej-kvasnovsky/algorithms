# Analysis of Algorithms

Consider these questions to be solved:

* Given N distinct integers, how many zeros is there?

* Given N distinct integers, how many combination of two sum to exactly zero?

* Given N distinct integers, how many triples sum to exactly zero?

Lets look at Java code that would be a first quick and dirty answer for given problem.

### Given N distinct integers, how many zeros is there?

O\(n\)

```
class Zeros {

    public int findZeros(int[] arr) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            if (i == 0) {
                count++;
            }
        }
        return count;
    }
}
```

### Given N distinct integers, how many combination of two sum to exactly zero?

O\(n^2\)

```
class Doubles {

    public int findZeroSums(int[] arr) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[i] + arr[j] == 0) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

### Given N distinct integers, how many triples sum to exactly zero?

O\(n^3\)

```
class Triplets {

    public int findZeroSums(int[] arr) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                for (int k = j + 1; k < arr.length; k++) {
                    if (arr[i] + arr[j] + arr[k] == 0) {
                        count++;
                    }
                }
            }
        }
        return count;
    }
}
```

Here is table that contains all basic classifications of Big-O complexity.

![](/assets/Screen Shot 2017-06-19 at 7.13.17 PM.png)

Here is a short overview of Big-O complexity classifications.![](/assets/Screen Shot 2017-06-19 at 7.11.45 PM.png)

### Binary Search

If we have sorted array, we can perform binary search. We go into the middle of array, if equal, we found it, if smaller, go left, if bigger go right.

```
class BS {

    int find(int[] arr, int value) {

        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            // here we divide it in half, and thus it is O(log n)
            int middle = low + ((high - low) / 2); 
            if (value < arr[middle]) {
                // go left
                high = middle - 1;
            } else if (value > arr[middle]) {
                // go right
                low = middle + 1;
            } else {
                // found!
                return middle;
            }
        }

        return -1;
    }
}

public class BinarySearch {

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 6, 8, 10, 20, 50, 100};

        BS bs = new BS();
        int index3 = bs.find(arr, 4);
        System.out.println(index3);

        int index5 = bs.find(arr, 8);
        System.out.println(index5);

        int index8 = bs.find(arr, 50);
        System.out.println(index8);

        int notFound = bs.find(arr, 200);
        System.out.println(notFound);
    }
}
```



