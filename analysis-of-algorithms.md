# Analysis of Algorithms

> It is convenient to have a measure of the amount of work involved in a computing process, even though it be a verycrudeone. We may count up the number of times that various elementary operations are applied in the whole process and then given them various weights. We might, for instance, count the number of additions, subtractions, multiplications, divisions, recording of numbers, and extractions of figures from tables. In the case of computing with matrices most of the work consists of multiplications and writting down numbers, andwe shall therefore only attempt to count the number of multiplications and recordings.
>
> — Alan Turing

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

### 3SUM problem with Binary Search

We use binary search for finding k index of a value that is opposite to what is at position i and j. So we calculate -arr\[i\] - arr\[j\] and then we search for this value in the array. That means -arr\[i\] - arr\[i\] + arr\[k\] is equal to 0.

O\(n^2 n log\(n\)\), definitelly better than O\(n^3\).

```
class TripletsWithBinarySearch {

    public int findZeroSums(int[] arr) {
        Arrays.sort(arr); // quick sort -> O(n log(n))

        int count = 0;
        int length = arr.length;
        for (int i = 0; i < length - 2; i++) { // O(n^2 n log(n))
            for (int j = i + 1; j < length - 1; j++) {
                int key = -arr[i] - arr[j];
                int k = Arrays.binarySearch(arr, j + 1, length, key);
                if (k > j && arr[k] - key == 0) { // compare index of found with current position (j)
                // this 'arr[k] - key == 0' part is actually useless, but it makes it easier to understand it
                    count++;
                }
            }
        }
        return count;
    }
}

public class SumInArray {

    public static void main(String[] args) {
        int[] arr = {0, 1, 2, -1, -2, 0, 5, 7};

        // O(n^2 logn)
        int tripletsBS = new TripletsWithBinarySearch().findZeroSums(arr);
        System.out.println(tripletsBS);
    }
}
```

[Here](https://gist.github.com/st0le/5893435) is another implementation of the problem.

### Memory

Typical memory consumption. ![](/assets/Screen Shot 2017-06-20 at 9.59.55 PM.png)



