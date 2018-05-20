# Minimum Index Sum of Two Lists

Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their **common interest **with the **least list index sum**. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

**Example 1:**

```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".
```

**Example 2:**

```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
```

**Note:**

1. The length of both lists will be in the range of \[1, 1000\].
2. The length of strings in both lists will be in the range of \[1, 30\].
3. The index is starting from 0 to the list length minus 1.
4. No duplicates in both lists.

Here is a solution using hash maps. 

```
class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        Map<String, Integer> m1 = new HashMap<>();
        for (int i = 0; i < list1.length; i++) {
            m1.put(list1[i], i);
        }
        
        Map<Integer, List<String>> sums = new HashMap<>();
        for (int i = 0; i < list2.length; i++) {
            String value = list2[i];
            if (m1.containsKey(value)) {
                Integer position = m1.get(value);
                int sum = position + i;
                if (!sums.containsKey(sum)) {
                    sums.put(sum, new ArrayList<>());
                }
                sums.get(sum).add(value);
            }
        }
        
        int min = Integer.MAX_VALUE;
        
        for (Integer key : sums.keySet()) {
            if (key < min) {
                min = key;
            }
        }
        return sums.get(min).toArray(new String[0]);
    }
}
```



