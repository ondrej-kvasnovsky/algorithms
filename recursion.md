# Recursion

Lets create a simple method that will use recursion to calculate sum of all numbers contained in an array. 

> We won't be able to get sum of large arrays with many items because of limitations of Java.

```
class Recursion {

    public static void main(String[] args) {
        Recursion recursion = new Recursion();

        int sum1 = recursion.sum(new int[]{1}, 0);
        System.out.println(sum1);

        int sum2 = recursion.sum(new int[]{1, 2, 3}, 0);
        System.out.println(sum2);
    }

    int sum(int[] array, int index) {
        if (index >= array.length) return 0;
        int value = array[index];
        return value + sum(array, ++index);
    }
}
```



