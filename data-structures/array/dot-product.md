# Dot Product

[Dot Product](https://en.wikipedia.org/wiki/Dot_product) is single number that is created by multiplication of two vectors \(two arrays\) of the same length.

```
public class DotProduct {

    public static void main(String... args) {
        int[] a = new int[]{ 0, 0, 0, 0, 1, 0, 5 }; // 2
        int[] b = new int[]{ 1, 0, 0, 0, 3, 0, 1 }; // 3

        int dot = dot(a, b);
        System.out.println(dot);

    }

    public static int dot(int[] v1, int[] v2) {
        if (v1.length != v2.length) {
            throw new RuntimeException("vectors must be of the same size");
        }

        int result = 0;
        for (int i = 0; i < v1.length; i++) {
            result += v1[i] * v2[i];
        }

        return result;
    }
}
```

We can see that the product of those to arrays is 8.

### Sparse Vector

For sparse vectors, that contain a lot of 0s, we might safe some time and before we process them, we could compress them.

The first idea I came up with was to create buckets of 0. For this array `{ 0, 0, 0, 0, 1, 0, 5 }`  we I could say there is a bucket of 0s from 0 to 3rd position. And then from 5th to 5th position.

Here is the attempt to implement that. The advantage is that we don't have to compress both arrays, but just one.

```
import java.util.ArrayList;
import java.util.List;

public class DotProduct {

    public static void main(String... args) {
        DotProduct dp = new DotProduct();

        int[] a = new int[]{ 0, 0, 0, 0, 1, 0, 5 };
        int[] b = new int[]{ 1, 0, 0, 0, 3, 0, 1 };

        List<Bucket> aCompressed = dp.compress(a);
        System.out.println(aCompressed);

        List<Bucket> bCompressed = dp.compress(b);
        System.out.println(bCompressed);

        int dot = dp.dot(aCompressed, b);
        System.out.println(dot);
    }

    class Bucket {
        int start;
        int end;
        int value;

        Bucket(int start, int end, int value) {
            this.start = start;
            this.end = end;
            this.value = value;
        }

        public String toString() {
            return String.format("%d: (%d, %d)", value, start, end);
        }
    }

    public List<Bucket> compress(int[] array) {
        List<Bucket> result = new ArrayList<>();

        // create bucket, while the value == 0, change end to index
        // else write bucket into result
        Bucket bucket = new Bucket(0, 0, 0);
        for (int i = 0; i < array.length; i++) {
            if (array[i] == 0) {
                if (bucket.value != 0) {
                    result.add(bucket);
                    bucket = new Bucket(i, i, array[i]);
                } else {
                    bucket.end = i;
                }
            } else {
                result.add(bucket);
                bucket = new Bucket(i, i, array[i]);
            }
        }
        result.add(bucket);

        return result;
    }

    public int dot(List<Bucket> a, int[] b) {
        int result = 0;

        for (int i = 0; i < a.size(); i++) {
            Bucket aBucket = a.get(i);
            if (aBucket.value != 0) {
                int bValue = b[aBucket.start];
                result += aBucket.value * bValue;
            }
        }

        return result;
    }
```

Then we get the following output.

```
[0: (0, 3), 1: (4, 4), 0: (5, 5), 5: (6, 6)]
[0: (0, 0), 1: (0, 0), 0: (1, 3), 3: (4, 4), 0: (5, 5), 1: (6, 6)]
8
```

When we look at that, we find that we didn't need start index at all. With this approach, it might be better to just create an index array that would keep indexes of the values.

```
import java.util.ArrayList;
import java.util.List;

public class DotProduct {

    public static void main(String... args) {
        DotProduct dp = new DotProduct();

        int[] a = new int[]{0, 0, 0, 0, 1, 0, 5};
        int[] b = new int[]{1, 0, 0, 0, 3, 0, 1};

        int[] index = dp.index(a, b);
        int dot2 = dp.dot(a, b, index);
        System.out.println(dot2);
    }

    public int dot(int[] a, int[] b, int[] index) {
        int result = 0;
        for (int i = 0; i < index.length; i++) {
            int indexValue = index[i];
            result += a[indexValue] * b[indexValue];
        }
        return result;
    }

    public int[] index(int[] a, int[] b) {
        List<Integer> temp = new ArrayList<>();

        for (int i = 0; i < a.length; i++) {
            if (a[i] != 0 && b[i] != 0) {
                temp.add(i);
            }
        }

        int[] result = new int[temp.size()];
        for (int i = 0; i < result.length; i++) {
            result[i] = temp.get(i);
        }
        return result;
    }
}
```



