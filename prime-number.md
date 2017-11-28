# Prime Number

Lets write a simple program that will verify if a number is prime number.

```
public class PrimeNumber {

    @Test
    public void generates_firstPrimeNumber() {
        Assert.assertFalse(isPrimeNumber(BigInteger.valueOf(0)));
        Assert.assertFalse(isPrimeNumber(BigInteger.valueOf(1)));
        Assert.assertTrue(isPrimeNumber(BigInteger.valueOf(2)));
        Assert.assertTrue(isPrimeNumber(BigInteger.valueOf(3)));
        Assert.assertFalse(isPrimeNumber(BigInteger.valueOf(4)));
        Assert.assertTrue(isPrimeNumber(BigInteger.valueOf(5)));
        Assert.assertFalse(isPrimeNumber(BigInteger.valueOf(6)));
    }

    private boolean isPrimeNumber(BigInteger number) {
        if (number.equals(ZERO) || number.equals(ONE)) return false;
        for (BigInteger i = BigInteger.valueOf(2); i.compareTo(number.subtract(ONE)) < 0; i = i.add(ONE)) {
            BigInteger remainder = number.remainder(i);
            if (remainder.equals(ZERO)) return false;
        }
        return true;
    }
}
```

Now lets try to verify if some big number is a primary number. Lets pick a random number like,

```
isPrimeNumber(new BigInteger("1001000000000000000000000000000000021"))
```

We find that that number is not prime number very quickly. Lets try to add 2 to that number.

```
isPrimeNumber(new BigInteger("1001000000000000000000000000000000023"))
```

Probably, you won't be able to find it in reasonable time. It takes really a lot of time.

## Find all prime numbers

If we would keep this algorithm run for few ethernities, we would maybe find the longest prime number so far discovered. This algorithm is the basic version, not optimized and thus very very slow type of algorithm.

```
public class PrimeNumber {
    @Test
    public void findsAllPrimeNumbers() {
        findAllPrimeNumbers(ZERO);
    }

    private boolean isPrimeNumber(BigInteger number) {
        if (number.equals(ZERO) || number.equals(ONE)) return false;
        for (BigInteger i = BigInteger.valueOf(2); i.compareTo(number.subtract(ONE)) < 0; i = i.add(ONE)) {
            BigInteger remainder = number.remainder(i);
            if (remainder.equals(ZERO)) return false;
        }
        return true;
    }

    private void findAllPrimeNumbers(BigInteger startFrom) {
        BigInteger runningNumber = startFrom;
        while (true) {
            if (isPrimeNumber(runningNumber))
                System.out.println("FOUND: " + runningNumber);
            runningNumber = runningNumber.add(ONE);
        }
    }
}
```

What would happen when we run the `findAllPrimeNumbers` with lests say `999999999999999999999999999999999`?

```
findAllPrimeNumbers(new BigInteger("999999999999999999999999999999999"));
```

We wouldn't get much far. It takes too much time to find number in single threaded process.

## Find prime numbers using multi threaded code

Another logical implication to speed up the search process is to use multiple CPUs to find the prime numbers. Lets say we want to create batches of 100 numbers and use 100 threads to find the numbers. We could write code like this to do it.

```
import org.junit.Assert;
import org.junit.Test;

import java.math.BigInteger;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.*;
import java.util.concurrent.atomic.AtomicReference;

import static java.math.BigInteger.ONE;
import static java.math.BigInteger.ZERO;

public class PrimeNumber {

    @Test
    public void findMultiThreaded() throws ExecutionException, InterruptedException, TimeoutException {
        // findAllPrimeNumbersMultiTheaded(ZERO);
        findAllPrimeNumbersMultiTheaded(new BigInteger("10000000"));
    }

    class FindPrimeNumber implements Callable<BigInteger> {
        private BigInteger candidate;

        public FindPrimeNumber(BigInteger candidate) {
            this.candidate = candidate;
        }

        @Override
        public BigInteger call() throws Exception {
            return isPrimeNumber(candidate);
        }

        private BigInteger isPrimeNumber(BigInteger number) {
            if (number.equals(ZERO) || number.equals(ONE)) return ZERO;
            for (BigInteger i = BigInteger.valueOf(2); i.compareTo(number.subtract(ONE)) < 0; i = i.add(ONE)) {
                BigInteger remainder = number.remainder(i);
                if (remainder.equals(ZERO)) return ZERO;
            }
            return number;
        }
    }

    private void findAllPrimeNumbersMultiTheaded(BigInteger startFrom) throws ExecutionException, InterruptedException, TimeoutException {
        ExecutorService executorService = Executors.newFixedThreadPool(1000);
        BigInteger runningNumber = startFrom;
        int counter = 0;
        int batchSize = 100;
        List<Callable<BigInteger>> tasks = new ArrayList<>();
        while (counter < batchSize) {
            tasks.add(new FindPrimeNumber(runningNumber));
            runningNumber = runningNumber.add(BigInteger.ONE);
            counter++;
            if (counter == batchSize) {
                List<Future<BigInteger>> futures = executorService.invokeAll(tasks);
                for (Future<BigInteger> future : futures) {
                    BigInteger foundNumber = future.get();
                    if (!foundNumber.equals(ZERO)) {
                        System.out.println("PRIME NUMBER:" + foundNumber);
                    }
                }
                counter = 0;
                tasks = new ArrayList<>();
            }
        }
    }

    class AtomicBigInteger {

        private final AtomicReference<BigInteger> valueHolder = new AtomicReference<>();

        public AtomicBigInteger(BigInteger bigInteger) {
            valueHolder.set(bigInteger);
        }

        public BigInteger incrementAndGet() {
            for (; ; ) {
                BigInteger current = valueHolder.get();
                BigInteger next = current.add(BigInteger.ONE);
                if (valueHolder.compareAndSet(current, next)) {
                    return next;
                }
            }
        }
    }
}
```

Here is a sample output this program produces. You can experiment with size of batch and number of threads if you like this brute force approach.

```
PRIME NUMBER:10000019
PRIME NUMBER:10000079
PRIME NUMBER:10000103
PRIME NUMBER:10000121
PRIME NUMBER:10000139
PRIME NUMBER:10000141
PRIME NUMBER:10000169
PRIME NUMBER:10000189
PRIME NUMBER:10000223
PRIME NUMBER:10000229
PRIME NUMBER:10000247
PRIME NUMBER:10000253
PRIME NUMBER:10000261
PRIME NUMBER:10000271
```

Be aware, if you are too eager with amount of threads and batch size, you will get this exception.

```
java.lang.OutOfMemoryError: unable to create new native thread
```



