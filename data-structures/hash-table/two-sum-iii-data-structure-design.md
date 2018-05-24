# Two Sum III - Data structure design

Design and implement a TwoSum class. It should support the following operations:`add`and`find`.

`add`- Add the number to an internal data structure.  
`find`- Find if there exists any pair of numbers which sum is equal to the value.

**Example 1:**

```
add(1); add(3); add(5);
find(4) -> true
find(7) -> false
```

**Example 2:**

```
add(3); add(1); add(2);
find(3) -> true
find(6) -> false
```

Here is a solution. 

```
class TwoSum {

    private List<Integer> values = new ArrayList<>();
    // private Set<Integer> values = new HashSet<>();
    
    /** Initialize your data structure here. */
    public TwoSum() {
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        values.add(number);
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        // Integer result = -(v - value);
        // if (values.contains(result)) {
        //     return true;
        // }
        Set<Integer> set = new HashSet<>();
        for (Integer v : values) { // 1, 3, 5 (4) -
            if (set.contains(v)) {
                return true;
            } else {
                Integer result = -(v - value);
                set.add(result);
            }
        }
        return false;
    }
}

/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * boolean param_2 = obj.find(value);
 */
```



