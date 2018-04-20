# Map

Map stores values behind keys. That said, values in a map can be obtained using a key.

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
        Entry<K, V> next;

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



