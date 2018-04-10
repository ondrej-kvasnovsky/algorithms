# Hash Table

Hash table offers a data structure that offers complexity of `O(1)` to insert and obtain element from it. We need to be able to calculate hash or position of element based on its value.

> If you are interesting in hash table practices, have a look at this [chapter in Java Handbook](https://ondrej-kvasnovsky.gitbooks.io/java-handbook/content/chapter1.html).

Lets create simple hash table to demonstrate how they are implemented. We can put couple of items into this hash table. If we would like to expand values array when more elements come, we would have to add more check and resizing. But this is omitted from this implementation for easier understanding.

```
import java.util.Arrays;

class HashTable {

    private String[] values;

    public HashTable() {
        values = new String[getMaxCapacity(10)];
    }

    public void put(String value) {
        int sizeMinusOne = values.length - 1;
        int position = sizeMinusOne & (value.hashCode() ^ (value.hashCode() >>> 16));
        values[position] = value;
    }

    public void remove(String value) {
        int sizeMinusOne = values.length - 1;
        int position = sizeMinusOne & (value.hashCode() ^ (value.hashCode() >>> 16));
        values[position] = null;
    }

    private int getMaxCapacity(int capacity) {
        int max = 1 << 30;
        int n = capacity - 1;
        n |= n >>> 1;
        n |= n >>> 2;
        n |= n >>> 4;
        n |= n >>> 8;
        n |= n >>> 16;
        return (n < 0) ? 1 : (n >= max) ? max : n + 1;
    }

    public int getCapacity() {
        return values.length;
    }

    public String toString() {
        return Arrays.toString(values);
    }
}
```

Now we can try to put and remove some elements.

```
public class HashTableDemo {

    public static void main(String[] args) {
        HashTable table = new HashTable();
        System.out.println(table.getCapacity());

        table.put("Hello");
        System.out.println(table);

        table.put("World");
        System.out.println(table);

        table.remove("World");
        System.out.println(table);

        table.put("123");
        System.out.println(table);

        table.put("1234");
        System.out.println(table);
    }
}
```

Observe how are the values placed in the array.

```
16
[null, null, null, null, Hello, null, null, null, null, null, null, null, null, null, null, null]
[null, null, null, null, Hello, null, null, null, null, null, null, null, World, null, null, null]
[null, null, null, null, Hello, null, null, null, null, null, null, null, null, null, null, null]
[null, null, 123, null, Hello, null, null, null, null, null, null, null, null, null, null, null]
[null, null, 123, null, Hello, 1234, null, null, null, null, null, null, null, null, null, null]
```



