# Map

Map stores values behind keys. That said, values in a map can be obtained using a key.

Lets create very simple hash map. This hash map is fixed size and does not count other types than integer. 

```
class MyHashMap {
    
    Integer[] values = new Integer[1000000];
   
    /** Initialize your data structure here. */
    public MyHashMap() {
    }
    
    /** value will always be positive. */
    public void put(int key, int value) {
        values[hash(key)] = value;
    }
    
    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    public int get(int key) {
        Integer result = values[hash(key)];
        if (result == null) {
            return -1;
        }
        return result;
    }
    
    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    public void remove(int key) {
        values[hash(key)] = null;
    }
    
    private int hash(int value) {
        return value % values.length;
    }
}
```

Now we can use the hash map as follows. 

```
MyHashMap hashMap = new MyHashMap();
hashMap.put(1, 1);          
hashMap.put(2, 2);         
hashMap.get(1);            // returns 1
hashMap.get(3);            // returns -1 (not found)
hashMap.put(2, 1);          // update the existing value
hashMap.get(2);            // returns 1 
hashMap.remove(2);          // remove the mapping for 2
hashMap.get(2);            // returns -1 (not found) 
```

## Implementation using Entry

We need to use Entry class to handle duplicates \(when two objects have the same hash code but they are not equal\). 

```
class HashMap<K, V> {
    private Entry[] entries;

    HashMap() {
        entries = new Entry[10];
    }

    public void put(K key, V value) {
        Entry<K, V> entry = new Entry<>(key, value);
        int position = calculateHashCode(key);
        if (entries[position] == null) {
            entries[position] = entry;
        } else {
            Entry<K, V> available = findNextAvailableEntry(position);
            available.next = entry;
        }
    }

    public V get(K key) {
        int position = calculateHashCode(key);
        Entry entry = entries[position];
        while (!entry.key.equals(key)) {
            entry = entry.next;
        }
        return (V) entry.value;
    }

    Entry<K, V> findNextAvailableEntry(int position) {
        Entry<K, V> current = entries[position];
        if (current.next != null) {
            current = current.next;
        }
        return current;
    }

    int calculateHashCode(K key) {
        return key.hashCode() % entries.length;
    }

    class Entry<K, V> {
        K key;
        V value;
        Entry<K, V> next; // linked list

        Entry(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }
}
```

Lets try to use the hash map.

```
public class Test {

    public static void main(String... args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("a", 1);
        map.put("b", 2);
        map.put("k", 3); // k has conflicting position 

        Integer one = map.get("a");
        System.out.println(one);

        Integer three = map.get("k");
        System.out.println(three);

        System.out.println("a: " + map.calculateHashCode("a"));
        System.out.println("b: " + map.calculateHashCode("b"));
        System.out.println("c: " + map.calculateHashCode("c"));
        System.out.println("d: " + map.calculateHashCode("d"));
        System.out.println("e: " + map.calculateHashCode("e"));
        System.out.println("f: " + map.calculateHashCode("f"));
        System.out.println("g: " + map.calculateHashCode("g"));
        System.out.println("h: " + map.calculateHashCode("h"));
        System.out.println("i: " + map.calculateHashCode("i"));
        System.out.println("j: " + map.calculateHashCode("j"));
        System.out.println("k: " + map.calculateHashCode("k"));
    }
}
```

How the position is calculated.

```
println "a".hashCode()
println "b".hashCode()
println "k".hashCode()
println "u".hashCode()

println "a".hashCode() % 10
println "k".hashCode() % 10
println "u".hashCode() % 10
```

Here is the output.

```
97
98
107
117

7
7
7
```



