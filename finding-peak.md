# Finding Peak

Lets find peak in various ways.

### Finding peak in an 1-D array

Consider a one dimensional array, `[a, b, c, d, e, f]`. `b` is a peak if and only `b >= a` and `b >= c`.

#### Easy and slow solution

Easy and slow algorighm to find a peak is to start the begging and do the check for peak. If it is found, return the index of peak value. This algorithm is O\(n\), which is too slow bigger arrays. 

```
public int findPeak(int[] array) {
    if (array.length == 1) return 0;
    if (array.length == 2) {
        if (array[0] >= array[1]) {
            return 0;
        } else if (array[0] < array[1]) {
            return 1;
        }
        return -1;
    }

    for (int i = 0; i < array.length; i++) {
        if (i == 0) {
            if (array[i] > array[i + 1]) {
                return i;
            }
            continue;
        }
        if (i == array.length -1) {
            if (array[i] > array[i - 1]) {
                return i;
            }
        }
        if (array[i] >= array[i - 1] && array[i] >= array[i + 1]) {
            return i;
        }
    }

    return -1;
}
```

Here are the test cases it passes. 

```
def 'returns -1 when array is empty'() {
    given:
    int[] array = []
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == -1
}
def 'finds peak in array of one item'() {
    given:
    int[] array = [1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 0
}
def 'finds peak in array of two items: 1, 2'() {
    given:
    int[] array = [1, 2]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 1
}
def 'finds peak in array of two items: 2, 1'() {
    given:
    int[] array = [2, 1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 0
}
def 'finds peak in array of two items: 1, 1'() {
    given:
    int[] array = [1, 1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 0
}
def 'finds peak in array of 3 items: 3, 2, 1'() {
    given:
    int[] array = [3, 2, 1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 0
}
def 'finds peak in array of 3 items: 2, 3, 1'() {
    given:
    int[] array = [2, 3, 1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 1
}
def 'finds peak in array of 3 items: 2, 1, 3'() {
    given:
    int[] array = [2, 1, 3]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 0
}
def 'finds peak in array of 3 items: 1, 1, 3'() {
    given:
    int[] array = [1, 1, 3]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 2
}
def 'finds peak in array of 3 items: 0, 1, 1'() {
    given:
    int[] array = [0, 1, 1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 1
}
def 'finds peak in array of 4 items: 1, 2, 3, 4'() {
    given:
    int[] array = [1, 2, 3, 4]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 3
}
def 'finds peak in array of 4 items: 1, 2, 3, 4, 3, 2, 1'() {
    given:
    int[] array = [1, 2, 3, 4, 3, 2, 1]
    when:
    int index = peakFinder.findPeak(array)
    then:
    index == 3
}
```

Since we have test cases, we can try to develop other solution, which should pass the same set of test cases. 

#### Faster solution using recursion and binary search

TODO

