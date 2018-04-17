# Fibonacci Sequence

Fibonacci sequence starts from 1. It is 1 1 2 3 5 8 11... and so on. 

Lets see how to get fibonacci sequence using while loop and recursion. 

```
public class Demo {

    public static void main(String... args) {
        // 1 2 3 4 5 6
        // 1 1 2 3 5 8
        System.out.println("Fib: " + fib(1)); // 1
        System.out.println("Fib: " + fib(2)); // 1
        System.out.println("Fib: " + fib(3)); // 3
        System.out.println("Fib: " + fib(6)); // 8

        System.out.println("fibRecursion: " + fibRecursion(1)); // 1
        System.out.println("fibRecursion: " + fibRecursion(2)); // 1
        System.out.println("fibRecursion: " + fibRecursion(5)); // 3
        System.out.println("fibRecursion: " + fibRecursion(8)); // 8
    }

    // without recursion
    private static int fib(int nth) {
        int index = nth - 2;
        int previous = 1;
        int current = 1;
        while (index > 0) {
            int sum = previous + current;
            previous = current;
            current = sum;
            System.out.println(sum);

            index--;
        }
        return current;
    }

    private static int fibRecursion(int nth) {
        if (nth == 0 || nth == 1) {
            return 1;
        }
        return fibRecursion(nth - 1) + fibRecursion(nth -2);
    }
}
```



