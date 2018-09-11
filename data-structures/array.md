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

Here is another example with `add`, `get` and `remove` functions.

```
package datastructures;

class ArrayListTest {
    public static void main(String[] a) {
        ArrayList<Integer> list = new ArrayList<>();

        System.out.println(list);

        list.add(1);
        System.out.println(list);

        list.add(2);
        System.out.println(list);

        list.add(3);
        System.out.println(list);

        System.out.println(list.get(0));

        list.remove(1);
        System.out.println(list);
    }
}

public class ArrayList<E> {
    private E[] values;
    private int initialSize = 10;
    private int count;

    public ArrayList() {
        values = (E[]) new Object[initialSize];
    }

    public void add(E value) {
        if (count >= values.length) {
            resize();
        }
        values[count++] = value;
    }

    public void resize() {
        initialSize *= 2;
        E[] t = (E[]) new Object[initialSize];
        System.arraycopy(values, 0, t, 0, values.length);
        values = t;
    }

    public E get(int index) {
        if (index < 0 || index >= count) throw new IndexOutOfBoundsException();
        return values[index];
    }

    public void remove(int index) {
        if (index < 0 || index >= count) throw new IndexOutOfBoundsException();
        values[index] = null;
        if (index < count - 1) {
            System.arraycopy(values, index + 1, values, index, count);
        }
        count--;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        for (int i = 0; i < count; i++) {
            sb.append(values[i]);
            if (i != count - 1) {
                sb.append(",");
            }
        }
        sb.append("]");
        return sb.toString();
    }
}

```



