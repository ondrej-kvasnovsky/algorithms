# Arrays

Arrays are usually fixed size collection of items. An array is a basic data structure that allocates memory that will hold our values. 

> To push the arrays to the limits and see that an array really allocates memory, try to create array of huge size, like `int[] hugeArray = new int[2000000000]`. We should get `java.lang.OutOfMemoryError: Java heap space` exception with default JVM memory settings.

```
import java.util.Arrays;

public class ArraysDemo {

    public static void main(String... args) {
        int[] array = new int[5];
        array[0] = 3;
        array[1] = 4;
        array[2] = 6;
        array[3] = 8;
        array[4] = 1;

        int sum = 0;
        for(Integer value : array) {
            sum += value;
        }
        System.out.println(String.format("Sum is %s", sum));

        System.out.println(Arrays.toString(array));

        Arrays.sort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

Here is the output. 

```
Sum is 22
[3, 4, 6, 8, 1]
[1, 3, 4, 6, 8]
```

# Lists

Lists are similar to arrays but they are dynamically expanding. Some languages do not distinguish between arrays and lists. A list implementations are using arrays to store values. 

Here is a naive implementation of list. This list resizes the array when all the positions in the array are occupied and user requests to insert another item into a list. 

```
import java.util.Arrays;

public class NaiveList {
    private String[] values = new String[5];
    private int currentIndex = 0;
    private int size = 0;

    public void add(String value) {
        if(size < values.length) {
            values[currentIndex++] = value;
            size++;
        } else {
            int newLength = values.length * 2;
            values = Arrays.copyOf(values, newLength);
            values[currentIndex++] = value;
            size++;
        }
    }

    public String get(int index) {
        return values[index];
    }

    public int size() {
        return size;
    }
}
```

We can use the naive implementation of list now. 

```
import java.util.Arrays;

public class ListsDemo {

    public static void main(String... args) {
        NaiveList list = new NaiveList();
        list.add("John 1");
        list.add("John 2");
        list.add("John 3");
        list.add("John 4");
        list.add("John 5");
        list.add("John 6");
        list.add("John 7");
        list.add("John 8");
        list.add("John 9");
        list.add("John 10");

        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }
}
```

Here is what the code above prints. 

```
John 1
John 2
John 3
John 4
John 5
John 6
John 7
John 8
John 9
John 10
```



