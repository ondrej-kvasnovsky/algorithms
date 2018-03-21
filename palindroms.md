# Palindroms

[Palindroms](https://en.wikipedia.org/wiki/Palindromic_number) are strings or numbers that start and end with the same character sequence, for example ABCBA or 12321.

## Lychrel Number

Every number that does not become palindrom after couple of interations is called [Lychrel number](https://en.wikipedia.org/wiki/Lychrel_number). Here is an example.

If we send there number like 1960000, it finds 3 palindroms in 1000 interactions. Interesting is that if we use 196 \(Lychrel number\), we are not able to find Palindrom \(nobody found one yet\).

```
boolean isPalindrom(String word) {
  int start = 0;
  int end = word.length() - 1;
  while (start < end) {
    if (word.charAt(start) != word.charAt(end)) {
      return false;
    }
    start++;
    end--;
  }
  return true;
}

BigInteger canidate = 1960000
BigInteger temp = canidate
(1..1000).forEach {
  temp = temp.add(new BigInteger(temp.toString().reverse()))
  if (isPalindrom(temp.toString())) {
    println "Iteration: $it found ${temp}"
  }
}
```

When we run this for 1960000, the algorithm finds the following palindroms.

```
Iteration: 1 found 1960691
Iteration: 5 found 27766772
Iteration: 12 found 8434774348
```



