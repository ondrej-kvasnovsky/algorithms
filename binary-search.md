### Binary Search

99% of binary search problems that you see online will fall into 1 of these 3 templates.

**Note:**The templates and their differences have been colored coded below.

![](https://leetcode.com/explore/learn/card/binary-search/135/template-iii/Figures/binary_search/Template_Diagram.png)

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

### Another ways to implement binary search

It is used to search for an element or condition which requires accessing the current index and its immediate right neighbor's index in the array.

```
int binarySearch(int[] nums, int target){
  if(nums == null || nums.length == 0)
    return -1;

  int left = 0;
  int right = nums.length;
  while (left < right) {
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if (nums[mid] == target) { 
        return mid; 
    }
    else if(nums[mid] < target) { 
        left = mid + 1; 
    } else { 
        right = mid; 
    }
  }

  // Post-processing:
  // End Condition: left == right
  if (left != nums.length && nums[left] == target) {
      return left;
  }
  return -1;
}
```

This is used when requires accessing the current index and its immediate left and right neighbor's index in the array.

```
int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0)
        return -1;

    int left = 0, right = nums.length - 1;
    while (left + 1 < right){
        // Prevent (left + right) overflow
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }

    // Post-processing:
    // End Condition: left + 1 == right
    if(nums[left] == target) return left;
    if(nums[right] == target) return right;
    return -1;
}
```

### 3SUM problem with Binary Search

We use binary search for finding `k` index of a value that is opposite to what is at position `i` and `j`. So we calculate `-arr[i] - arr[j]` and then we search for this value in the array. That means `-arr[i] - arr[i] + arr[k]` is equal to `0`.

`O(n^2 n log(n))`, definitelly better than `O(n^3)`.

```
import java.util.Arrays;

class TripletsWithBinarySearch {

    public int findZeroSums(int[] arr) {
        Arrays.sort(arr); // quick sort -> O(n log(n))

        int count = 0;
        int length = arr.length;
        for (int i = 0; i < length - 2; i++) { // O(n^2 n log(n))
            for (int j = i + 1; j < length - 1; j++) {
                int key = arr[i] + arr[j];
                int opposite = -key;
                int k = Arrays.binarySearch(arr, j + 1, length, opposite);
                if (k > j && arr[k] - opposite == 0) { // compare index of found with current position (j)
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

