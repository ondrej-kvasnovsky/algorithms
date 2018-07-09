# Merge Sorted Array

Given two sorted integer arrays _nums1 _and _nums2_, merge _nums2 _into _nums1 _as one sorted array.

**Note:**

* The number of elements initialized in _nums1 _and _nums2 _are _m _and _n _respectively.
* You may assume that _nums1 _has enough space \(size that is greater or equal to _m_+_n_\) to hold additional elements from _nums2_.

**Example:**

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## Solution

Easy and not efficient way is to just append the array and then sort it. 

```
public void merge(int[] nums1, int m, int[] nums2, int n) {
    for(int i = 0; i < n; i++) {
        nums1[m + i] = nums2[i];
    }
    Arrays.sort(nums1);
}
```

Other solution is to create new array and put there the values. Then just take the values and paste them into num1.

```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // 1 first idea, but I din't notice we have to write it into nums1, 
        // so I ended up copying arrays and the end
        // create index = 0 to store values in the new array
        // create new array of m+m size
        // mIndex and nIndex - incremented if value from that is added
        // read the array until n or m is bigger than or equal 0
        //   if m >= 0 && n >= 0 -> get values and compare -> if m is less than or equal, store m val on index possition, index++
        //   else if m >= 0 write m value
        //   else if n >= 0 write n value
        //   else write n and incement index 
        
        int index = 0;
        int[] result = new int[m + n];
        
        int mIndex = 0;
        int nIndex = 0;
        
        while (mIndex < m || nIndex < n) {
            if (mIndex < m && nIndex < n) {
                int mVal = nums1[mIndex];
                int nVal = nums2[nIndex];
                if (mVal <= nVal) {
                    result[index] = mVal;
                    mIndex++;
                } else {
                    result[index] = nVal;
                    nIndex++;
                }
            } else if (mIndex < m) {
                result[index] = nums1[mIndex];
                mIndex++;
            } else if (nIndex < n) {
                result[index] = nums2[nIndex];
                nIndex++;
            }
            index++;
        }
        
        for (int i = 0; i < result.length; i++) {
            nums1[i] = result[i];
        }
    }
}
```

Here is a solution that will do it in-place.

```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // go from the end of both arrays and write into result the higher value
        int index = m + n - 1;
        int index1 = m - 1;
        int index2 = n - 1;
        while (index1 >= 0 && index2 >= 0) {
            if (nums1[index1] > nums2[index2]) {
                nums1[index] = nums1[index1];
                index--;
                index1--;
            } else {
                nums1[index] = nums2[index2];
                index--;
                index2--;
            }
        }
        
        while (index2 >= 0) { // write remaining values, if any
            nums1[index] = nums2[index2];
            index--;
            index2--;
        }        
    }
}
```



