# Queue

Queue is first in last out.

We can implement it using the same approaches as in Stack, linked list or array. ![](/assets/Screen Shot 2017-06-22 at 12.37.56 AM.png)Solution

Here is an implementation of Queue in java. 

```
package datastructures;

public class QueueTest {

    public static void main(String[] args) {
        MyQueue q = new MyQueue();
        q.push(1);
        q.push(2);
        System.out.println(q.poll()); // 1
        q.push(3);
        System.out.println(q.poll()); // 2
        System.out.println(q.poll()); // 3
    }
}

class MyQueue {
    MyQueueNode head;
    MyQueueNode tail;

    void push(int i) {
        MyQueueNode n = new MyQueueNode(i);
        if (head == null) {
            head = n;
            tail = n;
        } else {
            tail.next = n;
            tail = n;
        }
    }

    int poll() {
        if (head == null) return -1;
        else {
            int val = head.val;
            head = head.next;
            return val;
        }
    }
}

class MyQueueNode {
    int val;
    MyQueueNode next;

    public MyQueueNode(int val) {
        this.val = val;
    }
}
```

 Here is a naive implementation of queue in Kotlin. If we know the items upfront, we could do this.

```
class Queue<T>(vararg items: T) {
    private val values = items.toMutableList()
    fun enqueue(item: T) {
        values.add(item)
    }

    fun dequeue(): T? {
        if (values.isNotEmpty()) {
            return values.removeAt(0)
        }
        return null
    }
}

fun <T> queueOf(vararg items: T): Queue<T> {
    return Queue(*items) // * is spread operator
}

fun main(args: Array<String>) {
    val queue = queueOf(1, 2)
    queue.enqueue(3)
    println(queue.dequeue())
    println(queue.dequeue())
    println(queue.dequeue())
    println(queue.dequeue())
}
```

Here is the output for illustration what is going on.

```
1
2
3
null
```



