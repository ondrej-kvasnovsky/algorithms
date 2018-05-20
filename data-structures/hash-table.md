# Set

Hash set offers a data structure that offers complexity of `O(1)` to insert and obtain element from it. We need to be able to calculate hash or position of element based on its value.

> If you are interesting in sets, have a look at this [chapter in Java Handbook](https://ondrej-kvasnovsky.gitbooks.io/java-handbook/content/chapter1.html).

Here is a naive implementation of hash set. 

```
class MyHashSet {
    
    private Integer[] values = new Integer[1000000];
    
    public void add(int key) {
        values[hash(key)] = key;
    }
    
    public void remove(int key) {
        values[hash(key)] = null;
    }
    
    /** Returns true if this set did not already contain the specified element */
    public boolean contains(int key) {
        return values[hash(key)] != null;
    }
    
    public int hash(int value) {
        return value % values.length;
    }
}
```

We can perform the following with the hash set we have created. 

```
MyHashSet hashSet = new MyHashSet();
hashSet.add(1);         
hashSet.add(2);         
hashSet.contains(1);    // returns true
hashSet.contains(3);    // returns false (not found)
hashSet.add(2);          
hashSet.contains(2);    // returns true
hashSet.remove(2);          
hashSet.contains(2);    // returns false (already removed)
```

## Advanced hashing and re-sizing hash set. 

Lets create simple hash set to demonstrate how they are implemented. We can put couple of items into this hash set. If we would like to expand values array when more elements come, we would have to add more check and resizing. But this is omitted from this implementation for easier understanding.

```
import java.util.Arrays;

class HashSet {

    private String[] values;

    public HashSet() {
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
public class HashSetDemo {

    public static void main(String[] args) {
        HashSet set = new HashSet();
        System.out.println(set.getCapacity());

        set.put("Hello");
        System.out.println(set);

        set.put("World");
        System.out.println(set);

        set.remove("World");
        System.out.println(set);

        set.put("123");
        System.out.println(set);

        set.put("1234");
        System.out.println(set);
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



