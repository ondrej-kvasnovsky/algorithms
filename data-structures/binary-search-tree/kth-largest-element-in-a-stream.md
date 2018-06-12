# Kth Largest Element in a Stream

Design a class to find the **k**th largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Your `KthLargest` class will have a constructor which accepts an integer`k`and an integer array`nums`, which contains initial elements from the stream. For each call to the method`KthLargest.add`, return the element representing the kth largest element in the stream.

**Example:**

```
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

**Note:**  
You may assume that `nums`' length ≥ `k-1` and`k`≥ 1.

## Solution for an array

Sort values. 

```
public int findKthLargest(int[] nums, int k) {
    int N = nums.length;
    Arrays.sort(nums);
    return nums[N - k];
}
```

Using priority queue. 

```
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue queue = new PriorityQueue<>(new Comparator() {
            @Override
            public int compare(Integer num1, Integer num2) {
                return (num2 - num1);
            }
        });
        for(int val : nums)
            queue.offer(val);
        for(int i = 0; i < k-1; i++)
            queue.poll();
        return queue.poll();
        
    }
```

## Solution for a stream



```

```



