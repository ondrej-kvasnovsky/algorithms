# Find Sum in Array

Lets start from simple search algorithms to more advanced.

### Find Zeros `O(n)`

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

### Two Sum `O(n^2)`

```
 class TwoSum {

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

### Two Sum `O(n)`

```
class TwoSumWithHashMap {

    public int[] findSums(int[] arr, int target) {
        // iterate trough the array {0, 1, 2, -1, -2, 0, 5, 7}
        // calculate difference between value from array and target, 0 - 0 = 0
        //   if 0 is contained, return index of current and value from map (which is index of that value)
        //   else put it into map, result is the key and i (index) is the value
        Map<Integer, Integer> temp = new HashMap<>();

        for (int i = 0; i < arr.length; i++) {
            int number = arr[i]; // 2, 7, 11, 15
            // 9 - 2 = 7 -> store 2
            // 9 - 7 = 2 -> temp contains 2, so the sum is found
            // 9 - 11 = -2
            // 9 - 15 = -6
            int difference = target - number;
            if (temp.containsKey(difference)) {
                return new int[] { temp.get(difference), i };
            }
            temp.put(number, i);
        }

        return null;
    }
}
```

### Three Sum `O(n^3)`

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

### Three Sum `O(n^2logn)`

```
 class TripletsWithBinarySearch {

    public int findZeroSums(int[] arr) {
        Arrays.sort(arr); // O(n log(n))

        int count = 0;
        int length = arr.length;
        for (int i = 0; i < length - 2; i++) {
            for (int j = i + 1; j < length - 1; j++) {
                int key = -arr[i] - arr[j];
                int k = Arrays.binarySearch(arr, j + 1, length, key);
                if (k > j && arr[k] - key == 0) { // compare index of found with current position (j)
                    count++;
                }
            }
        }
        return count;
    }
}
```



