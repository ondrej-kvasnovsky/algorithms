# First Bad Version

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have`n`versions`[1, 2, ..., n]`and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API`bool isBadVersion(version)`which will return whether`version`is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example:**

```
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version. 
```

## Solution

```
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        // versions are sorted, if we find bad version, all versions after that are bad
        // 1) "binary search"
        // badVersion = -1
        // go to middle -> is it bad? -> check left side (continue binary search)
        //              -> is good -> check right side
        // start position is the bad version then
        int start = 1;
        int end = n;
        while (start < end) {
            int middle = start + (end - start) / 2; // 0 + (4 - 1) / 2 -> 2, 0 + (5 - 1) / 2 -> 3
            boolean isBad = isBadVersion(middle);
            if (isBad) {
                end = middle;
            } else {
                start = middle + 1;
            }   
        }
        return start;
    }
}
```



