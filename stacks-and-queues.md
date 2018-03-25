# Stacks and Queues

Stack is first in first out. Queue is first in last out.![](/assets/Screen Shot 2017-06-22 at 12.37.56 AM.png)Stack

In order to impelment stack, we could use an array \(but we would have to take care of resizing\) or we could use linked list.

Linked list is probably going to take more memory than array implementation. But with array implementation, we need to resize or limit stack. Also in array approach, there could be issue with holding an item in memory even it is not used \(so, array approach could take more memory than linked list approach\).

When using array approach, we should expand an array when the array is 25% or something like that, full. That will prevent often shrinking and expanding of an array.

```
class Stack<T>(vararg items: T) {
    private val values = items.toMutableList()
    fun push(item: T) {
        values.add(item)
    }

    fun pop(): T? {
        if (values.isNotEmpty()) {
            val size = values.size
            return values.removeAt(size - 1)
        }
        return null
    }
}

fun <T> stackOf(vararg items: T): Stack<T> {
    return Stack(*items) // * is spread operator
}

fun main(args: Array<String>) {
    val stack = stackOf(1, 2)
    stack.push(3)
    println(stack.pop())
    println(stack.pop())
    println(stack.pop())
    println(stack.pop())
}
```

Here is the output for illustration what is going on. 

```
3
2
1
null
```

### Queue

We can implement it using the same approaches as in Stack, linked list or array.

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



