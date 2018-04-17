# Duplicate Counts

The idea is: put all items into a map, if an item exists, increase value behind a key. Ideally, sort the tree by value \(it results in not very straight forward solution in Java\).

```
import java.util.*;
import java.util.stream.Collectors;

public class DuplicateCounts {

    public static void main(String... args) {
        int[] array = new int[]{3, 3, 3, 3, 2, 2, 4, 5, 1, 1, 1};

        Map<Integer, Integer> counts = new TreeMap<>();
        for (Integer item : array) {
            if (counts.containsKey(item)) {
                counts.computeIfPresent(item, (key, value) -> value + 1);
            } else {
                counts.put(item, 1);
            }
        }

        System.out.println(counts);

        // sort by values
        Comparator<Integer> comparator = (key1, key2) -> {
            System.out.println(key1 + " - " + key2);
            Integer value1 = counts.get(key1);
            Integer value2 = counts.get(key2);
            System.out.println(value1 + ", " + value2);
            int result = value2.compareTo(value1); // if values are the same, use keys, otherwise entry will be not inserted into the treemap
            return result == 0 ? key2.compareTo(key1) : result;
        };
        TreeMap<Integer, Integer> sortedByValue = new TreeMap<>(comparator);
        sortedByValue.putAll(counts);
        System.out.println(sortedByValue);

        // sort using streams
        List<Map.Entry<Integer, Integer>> sorted = counts.entrySet()
                .stream()
                .sorted(Collections.reverseOrder(Map.Entry.comparingByValue()))
                .collect(Collectors.toList());
        System.out.println(sorted);
    }
}
```



