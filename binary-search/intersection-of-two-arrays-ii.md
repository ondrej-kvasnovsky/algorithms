# Intersection of Two Arrays II

Given two arrays, write a function to compute their intersection.

**Example:**  
Given nums1=`[1, 2, 2, 1]`, nums2=`[2, 2]`, return`[2, 2]`.

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

## Solution

```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        // iterate through the bigger arra and make counts
        // take the smaller array for comparison to speed it up
        // for each found number, take it, write it into result and decrement by 1
        int[] bigger;
        int[] smaller;
        if (nums1.length > nums2.length) {
            bigger = nums1;
            smaller = nums2;
        } else {
            bigger = nums2;
            smaller = nums1;
        }
        
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < bigger.length; i++) {
            int number = bigger[i];
            int count = map.getOrDefault(number, 0);
            map.put(number, count + 1);
        }
        
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < smaller.length; i++) {
            int number = smaller[i];
            if (map.containsKey(number)) {
                int count = map.get(number);
                if (count > 0) {
                    result.add(number);
                    map.put(number, count - 1);
                }
            }
        }
        
        int[] r = result.stream().mapToInt(Integer::intValue).toArray();
        return r;
    }
}
```

Another solution which is O\(n log n\).

```
public class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        if(nums1.length==0||nums2.length==0)
            return new int[0];
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int p1=0;
        int p2=0;
        List<Integer> res=new ArrayList<Integer>();
        while(p1<nums1.length && p2<nums2.length){
            if(nums1[p1]==nums2[p2]){
                res.add(nums1[p1]);
                p1++;
                p2++;
            }
            else if(nums1[p1]<nums2[p2])
                p1++;
            else 
                p2++;
        }
        int[] t=new int[res.size()];
        for(int i=0;i<res.size();i++)
            t[i]=res.get(i);
            
        return t;
    }
}
```



