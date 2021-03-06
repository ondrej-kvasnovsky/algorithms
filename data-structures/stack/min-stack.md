# Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* getMin\(\) -- Retrieve the minimum element in the stack.

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## Solution

One idea is to use two data structures. Stack for stack and for minimal value priority queue.

```
class MinStack {

    Stack<Integer> stack = new Stack<>();
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    /** initialize your data structure here. */
    public MinStack() {
    }

    public void push(int x) {
        stack.push(x);
        minHeap.add(x);
    }

    public void pop() {
        Integer popped = stack.pop();
        minHeap.remove(popped);
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minHeap.peek();
    }
}
```

Solution without using any existing data structures. 

```
class MinStack {
    private Node head;
    
    public void push(int x) {
        if(head == null) {
            head = new Node(x, x);
        } else {
            head = new Node(x, Math.min(x, head.min), head);
        }
    }

    public void pop() {
        head = head.next;
    }

    public int top() {
        return head.val;
    }

    public int getMin() {
        return head.min;
    }
    
    private class Node {
        int val;
        int min;
        Node next;
        
        private Node(int val, int min) {
            this(val, min, null);
        }
        
        private Node(int val, int min, Node next) {
            this.val = val;
            this.min = min;
            this.next = next;
        }
    }
}
```



