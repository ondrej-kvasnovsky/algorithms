# Queue

Queue is first in last out.

We can implement it using the same approaches as in Stack, linked list or array. ![](/assets/Screen Shot 2017-06-22 at 12.37.56 AM.png)

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



