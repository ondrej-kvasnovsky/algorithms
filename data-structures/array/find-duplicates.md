# Find Duplicates

We can put all items into set and then compare sized. If sizes are the same, there are not duplicates. 

```
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

public class Demo {

    public static void main(String... args) {
        Integer[] array = new Integer[]{1, 2, 3, 4, 5, 1};

        List<Integer> ints = Arrays.asList(array);
        Set<Integer> unique = new HashSet<>(ints);

        boolean containsDuplicate = ints.size() != unique.size();
        System.out.println(containsDuplicate);
    }
}
```



