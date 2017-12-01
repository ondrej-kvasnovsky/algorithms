# Prime factor {#firstHeading}

[Prime factor](https://en.wikipedia.org/wiki/Prime_factor) is a positive [integer](https://en.wikipedia.org/wiki/Integer) are the [prime numbers](https://en.wikipedia.org/wiki/Prime_number) that divide that integer exactly. For example, 8 is 2 \* 2 \* 2.

```
public class PrimeFactor {

    @Test
    public void test() {
        Assert.assertArrayEquals(primeFactor(1).toArray(), new Object[]{});
        Assert.assertArrayEquals(primeFactor(2).toArray(), new Object[]{2});
        Assert.assertArrayEquals(primeFactor(4).toArray(), new Object[]{2, 2});
        Assert.assertArrayEquals(primeFactor(8).toArray(), new Object[]{2, 2, 2});
    }

    private List<Integer> primeFactor(int n) {
        ArrayList<Integer> factors = new ArrayList<>();
        int divisor = 2;
        while (n > 1) {
            for (; n % divisor == 0; n /= divisor)
                factors.add(divisor);
        }
        return factors;
    }
}
```



