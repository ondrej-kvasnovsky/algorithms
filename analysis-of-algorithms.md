# Analysis of Algorithms

Consider these questions to be solved: 

* Given N distinct integers, how many zeros is there?

* Given N distinct integers, how many combination of two sum to exactly zero?

* Given N distinct integers, how many triples sum to exactly zero?

Lets look at Java code that would be a first quick and dirty answer for given problem. 

### Given N distinct integers, how many zeros is there?

O\(n\)

```
class Zeros {

    public int findZeros(int[] arr) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            if (i == 0) {
                count++;
            }
        }
        return count;
    }
}
```

### Given N distinct integers, how many combination of two sum to exactly zero?

O\(n^2\)

```
class Doubles {

    public int findZeroSums(int[] arr) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[i] + arr[j] == 0) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

### Given N distinct integers, how many triples sum to exactly zero?

O\(n^3\)

```
class Triplets {

    public int findZeroSums(int[] arr) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                for (int k = j + 1; k < arr.length; k++) {
                    if (arr[i] + arr[j] + arr[k] == 0) {
                        count++;
                    }
                }
            }
        }
        return count;
    }
}
```

Here is table that contains all basic classifications of Big-O complexity.

![](/assets/Screen Shot 2017-06-19 at 7.13.17 PM.png)



Here is a short overview of Big-O complexity classifications.![](/assets/Screen Shot 2017-06-19 at 7.11.45 PM.png)

