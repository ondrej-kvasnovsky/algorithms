# p^k

```
package math;

public class Pow {

    public static void main(String[] args) {
        System.out.println("Result: " + powN(2, 2));
        System.out.println("Result: " + powN(2, 10));
//        System.out.println("Result: " + powN(2, 50));

        System.out.println("Result: " + powLogN(2, 2));
        System.out.println("Result: " + powLogN(2, 10));
//        System.out.println("Result: " + powLogN(2, 50));
    }

    // O(n)
    public static long powN(long base, long exponent) {
        // e: 2 -> 2*2
        // e: 3 -> 2*2*2
        long result = 1;
        for (int i = 0; i < exponent; i++) {
            System.out.println(result);
            result *= base;
        }
        return result;
    }

    // O(log n)
    public static long powLogN(long base, long exponent) {
        System.out.println(base + " ^ " + exponent);
        if (exponent == 0) return 1;
        if (exponent % 2 == 0) {
            long l = powLogN(base * base, exponent / 2);
            return l;
        } else {
            long l = base * powLogN(base * base, (exponent - 1) / 2);
            return l;
        }
    }
}

```

Here is the output. 

```
O(n):

1
2
Result: 4

1
2
4
8
16
32
64
128
256
512
Result: 1024


O(log n): 

2 ^ 2
4 ^ 1
16 ^ 0
Result: 4

2 ^ 10
4 ^ 5
16 ^ 2
256 ^ 1
65536 ^ 0
Result: 1024
```



