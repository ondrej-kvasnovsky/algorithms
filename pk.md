# p^k



```
public class Pow {

    public static void main(String[] args) {
        System.out.println(powN(2, 2));
        System.out.println(powN(2, 10));
        System.out.println(powN(2, 50));

        System.out.println(powN(2, 2));
        System.out.println(powN(2, 10));
        System.out.println(powN(2, 50));
    }

    // O(n)
    public static long powN(long base, long exponent) {
        // e: 2 -> 2*2
        // e: 3 -> 2*2*2
        long result = 1;
        for (int i = 0; i < exponent; i++) {
            result *= base;
        }
        return result;
    }

    // O(n)
    public static long powLogN(long base, long exponent) {
        if (exponent == 0) return 1;
        if (exponent % 2 == 0) return powLogN(base, exponent / 2);
        else return base * powLogN(base, (exponent - 1) / 2);
    }
}
```



