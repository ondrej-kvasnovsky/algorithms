# Top K Frequent Elements

Given a non-empty array of integers, return the**k**most frequent elements.

For example,  
Given`[1,1,1,2,2,3]`and k = 2, return`[1,2]`.

**Note:**

* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity **must be **better than O\(n log n\), where n is the array's size.

Here is a solution. 

```
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        // create hash map and count frequency of all elements O(n) {1:3, 2:2, 3:1}
        // then sort the elements by value and get the top K elements
        Map<Integer, Integer> map = new HashMap<>();
        for (int i : nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        
        return map.entrySet()
            .stream()
            .sorted((a, b) -> b.getValue() - a.getValue())
            .map(entry -> entry.getKey())
            .limit(k)
            .collect(Collectors.toList());
    }
}
```



