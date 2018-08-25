# Mergesort

Complexity: O\(n log n\)

### Basic algorithm

* divide array in to two halves
* recursively sort each half 
  * recursively start dividing the first half, when you get into two
* merge two halfs

![](/assets/Screen Shot 2017-10-28 at 1.23.05 PM.png)

## Solution

Here is a solution I was able to develop. It could be optimized, we create temp array for every merge, it could be created only once at the beginning.

```
package sorting;

import java.util.Arrays;

public class MergeSort3 {

    public static void main(String[] args) {
        int[] sortedArray = {4, 5, 1, 2};
        mergeSortedArrays(sortedArray, 0, sortedArray.length / 2, sortedArray.length - 1);
        System.out.println(Arrays.toString(sortedArray));

        int[] array = {5, 4, 3, 2, 1, 100, -1};
        sort(array, 0, array.length - 1);
        System.out.println(Arrays.toString(array));
    }

    static void sort(int[] array, int left, int right) {
        if (left < right) {
            int middle = (left + right) / 2;
            sort(array, left, middle);
            sort(array, middle + 1, right);
            mergeSortedArrays(array, left, middle + 1, right);
        }
    }

    static void mergeSortedArrays(int[] array, int left, int middle, int right) {
        int[] temp = new int[array.length];

        int index = left;
        int index1 = left;
        int index2 = middle;

        while (index1 < middle && index2 <= right) {
            if (array[index1] <= array[index2]) {
                temp[index] = array[index1];
                index++;
                index1++;
            } else {
                temp[index] = array[index2];
                index++;
                index2++;
            }
        }
        while (index1 < middle) {
            temp[index] = array[index1];
            index++;
            index1++;
        }
        while (index2 < right) {
            temp[index] = array[index2];
            index++;
            index2++;
        }
        for (int i = left; i <= right; i++) {
            array[i] = temp[i];
        }
    }
}
```

Here is another implementation.

```
class MergerSort2 {
    public static void main(String[] args) {
        Integer[] a = {2, 6, 3, 5, 1};
        mergeSort(a);
        System.out.println(Arrays.toString(a));
    }

    public static void mergeSort(Comparable[] a) {
        Comparable[] tmp = new Comparable[a.length];
        mergeSort(a, tmp, 0, a.length - 1);
    }

    private static void mergeSort(Comparable[] a, Comparable[] tmp, int left, int right) {
        if (left < right) {
            int center = (left + right) / 2;
            mergeSort(a, tmp, left, center);
            mergeSort(a, tmp, center + 1, right);
            merge(a, tmp, left, center + 1, right);
        }
    }

    private static void merge(Comparable[] arr, Comparable[] tmp, int left, int right, int rightEnd) {
        int leftEnd = right - 1;
        int k = left;
        int num = rightEnd - left + 1;

        while (left <= leftEnd && right <= rightEnd)
            if (arr[left].compareTo(arr[right]) <= 0)
                tmp[k++] = arr[left++];
            else
                tmp[k++] = arr[right++];

        while (left <= leftEnd)    // Copy rest of first half
            tmp[k++] = arr[left++];

        while (right <= rightEnd)  // Copy rest of right half
            tmp[k++] = arr[right++];

        // Copy tmp back
        for (int i = 0; i < num; i++, rightEnd--)
            arr[rightEnd] = tmp[rightEnd];
    }
}
```

Here is another implementation. I have put it here just as a reference, but I don't like it. 

```
class MergeSort1 {
    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    void merge(int arr[], int l, int m, int r) {
        // Find sizes of two subarrays to be merged
        int n1 = m - l + 1;
        int n2 = r - m;

        /* Create temp arrays */
        int L[] = new int[n1];
        int R[] = new int[n2];

        /*Copy data to temp arrays*/
        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];


        /* Merge the temp arrays */

        // Initial indexes of first and second subarrays
        int i = 0, j = 0;

        // Initial index of merged subarry array
        int k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        /* Copy remaining elements of L[] if any */
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy remaining elements of R[] if any */
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    // Main function that sorts arr[l..r] using
    void sort(int arr[], int l, int r) {
        if (l < r) {
            // Find the middle point
            int m = (l + r) / 2;

            // Sort first and second halves
            sort(arr, l, m);
            sort(arr, m + 1, r);

            // Merge the sorted halves
            merge(arr, l, m, r);
        }
    }

    public static void main(String args[]) {
        int arr[] = {12, 11, 13, 5, 6, 7};

        System.out.println("Given Array");
        printArray(arr);

        MergeSort1 ob = new MergeSort1();
        ob.sort(arr, 0, arr.length - 1);

        System.out.println("\nSorted array");
        System.out.println(Arrays.toString(arr));
    }
}
```



