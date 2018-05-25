# Insert Delete GetRandom O\(1\)

Design a data structure that supports all following operations inaverage**O\(1\)**time.

1. `insert(val)`: Inserts an item val to the set if not already present.
2. `remove(val)`: Removes an item val from the set if present.
3. `getRandom`: Returns a random element from current set of elements. Each element must have the **same probability **of being returned.

**Example:**

```
// Init an empty set.
RandomizedSet randomSet = new RandomizedSet();

// Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomSet.insert(1);

// Returns false as 2 does not exist in the set.
randomSet.remove(2);

// Inserts 2 to the set, returns true. Set now contains [1,2].
randomSet.insert(2);

// getRandom should return either 1 or 2 randomly.
randomSet.getRandom();

// Removes 1 from the set, returns true. Set now contains [2].
randomSet.remove(1);

// 2 was already in the set, so return false.
randomSet.insert(2);

// Since 2 is the only number in the set, getRandom always return 2.
randomSet.getRandom();
```

Here is a solution. When we are removing, we want to find an element to remove. 

```
class RandomizedSet {
    
    // create list that contains unique values
    // create set that will make sure we work only with unique values
    private Set<Integer> set = new HashSet<>();
    private List<Integer> list = new ArrayList<>();
    
    public RandomizedSet() {
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        boolean added = set.add(val);
        if (added) {
            list.add(val);
        }
        return added;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        boolean removed = set.remove(val);
        if (removed) {
            for (int i = 0; i < list.size(); i++) {
                Integer value = list.get(i);
                if (value == val) {
                    list.remove(i);
                }
            }
        }
        return removed;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        Random r = new Random();
        int random = r.nextInt(list.size());
        return list.get(random);
    }

```

Other solution is to keep positions. Then we need to lower all position from the removed position in the list.

```
class RandomizedSet {

    private Map<Integer, Integer> positions = new HashMap<>();
    private List<Integer> list = new ArrayList<>();
    
    public RandomizedSet() {
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        boolean isContained = positions.containsKey(val);
        if (isContained) {
            return false;
        }
        list.add(val);
        positions.put(val, list.size() - 1);
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        boolean isContained = positions.containsKey(val);
        if (!isContained) {
            return false;
        }
        int position = positions.get(val);
        // go through all values that are above the removed value and lower the positon by 1
        for (int i = position; i < list.size(); i++) {
            int toBeLowered = list.get(i);
            int newVal = positions.get(toBeLowered) - 1;
            positions.put(toBeLowered, newVal);
        }
        list.remove(position);
        positions.remove(val);
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        Random r = new Random();
        int random = r.nextInt(list.size());
        return list.get(random);
    }
}
```



