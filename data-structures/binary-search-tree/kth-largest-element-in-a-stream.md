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

class KthLargest {
    // insert a node into the BST
    private Node insertNode(Node root, int num) {
        if (root == null) {
            return new Node(num, 1);
        }
        if (root.val < num) {
            root.right = insertNode(root.right, num);
        } else {
            root.left = insertNode(root.left, num);
        }
        root.cnt++;
        return root;
    }

    private int searchKth(Node root, int k) {
        // m = the size of right subtree
        int m = root.right != null ? root.right.cnt : 0;
        // root is the m+1 largest node in the BST
        if (k == m + 1) {
            return root.val;
        }
        if (k <= m) {
            // find kth largest in the right subtree
            return searchKth(root.right, k);
        } else {
            // find (k-m-1)th largest in the left subtree
            return searchKth(root.left, k - m - 1);
        }
    } 
    
    private Node root;
    private int m_k;

    public KthLargest(int k, int[] nums) {
        root = null;
        for (int i = 0; i < nums.length; ++i) {
            root = insertNode(root, nums[i]);
        }
        m_k = k;
    }
    
    public int add(int val) {
        root = insertNode(root, val);
        return searchKth(root, m_k);
    }
}

class Node {    // the structure for the tree node
    Node left;
    Node right;
    int val;
    int cnt;    // the size of the subtree rooted at the node
    public Node (int v, int c) {
        left = null;
        right = null;
        val = v;
        cnt = c;
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```



