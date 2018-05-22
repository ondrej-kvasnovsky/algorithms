# Logger Rate Limiter

Design a logger system that receive stream of messages along with its timestamps, each message should be printed if and only if it is **not printed in the last 10 seconds**.

Given a message and a timestamp \(in seconds granularity\), return true if the message should be printed in the given timestamp, otherwise returns false.

It is possible that several messages arrive roughly at the same time.

**Example:**

```
Logger logger = new Logger();

// logging string "foo" at timestamp 1
logger.shouldPrintMessage(1, "foo"); returns true; 

// logging string "bar" at timestamp 2
logger.shouldPrintMessage(2,"bar"); returns true;

// logging string "foo" at timestamp 3
logger.shouldPrintMessage(3,"foo"); returns false;

// logging string "bar" at timestamp 8
logger.shouldPrintMessage(8,"bar"); returns false;

// logging string "foo" at timestamp 10
logger.shouldPrintMessage(10,"foo"); returns false;

// logging string "foo" at timestamp 11
logger.shouldPrintMessage(11,"foo"); returns true;
```

Here is a solution. 

```
class Logger {
    
    private Map<String, Integer> values = new HashMap<>();

    public boolean shouldPrintMessage(int timestamp, String message) {
        System.out.println(values);
        if (values.containsKey(message)) {
            int previousTimestamp = values.get(message);
            if (timestamp - previousTimestamp < 10) {
                // it is still not more than 10s when the log was printed, return false
                return false;
            } else {
                values.put(message, timestamp); // update timestamp, it was print 10s or more seconds ago
                return true;
            }
        } else {
            // it is new, add it into map and return true because it is not contained in the map
            values.put(message, timestamp);
            return true;
        }
    }
}
```



