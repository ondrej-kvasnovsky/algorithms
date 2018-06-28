# Find Smallest Letter Greater Than Target

Given a list of sorted characters`letters`containing only lowercase letters, and given a target letter`target`, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is`target = 'z'`and`letters = ['a', 'b']`, the answer is`'a'`.

**Examples:**

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

**Note:**

1. `letters`has a length in range`[2, 10000]`
2. `letters`consists of lowercase letters, and contains at least 2 unique letters.
3. `target`is a lowercase letter.

## Solution

#### Approach \#1: Record Letters Seen {#approach-1-record-letters-seen-accepted}

**Intuition and Algorithm**

Let's scan through`letters`and record if we see a letter or not. We could do this with an array of size 26, or with a Set structure.

Then, for every next letter \(starting with the letter that is one greater than the target\), let's check if we've seen it. If we have, it must be the answer.

**Complexity Analysis**

* Time Complexity:O\(N\)O\(N\), whereNNis the length of`letters`. We scan every element of the array.

* Space Complexity:O\(1\)O\(1\), the maximum size of`seen`.

 

```
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        boolean[] seen = new boolean[26];
        for (char c: letters)
            seen[c - 'a'] = true;

        while (true) {
            target++;
            if (target > 'z') target = 'a';
            if (seen[target - 'a']) return target;
        }
    }
}
```

#### Approach \#2: Linear Scan {#approach-2-linear-scan-accepted}

**Intuition and Algorithm**

Since`letters`are sorted, if we see something larger when scanning form left to right, it must be the answer. Otherwise, \(since`letters`is non-empty\), the answer is`letters[0]`.

**Complexity Analysis**

* Time Complexity:O\(N\)O\(N\), whereNNis the length of`letters`. We scan every element of the array.

* Space Complexity:O\(1\)O\(1\), as we maintain only pointers.

```
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        for (char c: letters)
            if (c > target) return c;
        return letters[0];
    }
}
```

#### Approach \#3: Binary Search {#approach-3-binary-search-accepted}

**Intuition and Algorithm**

Like in_Approach \#2_, we want to find something larger than target in a sorted array. This is ideal for a_binary search_: Let's find the rightmost position to insert`target`into`letters`so that it remains sorted.

Our binary search \(a typical one\) proceeds in a number of rounds. At each round, let's maintain the_loop invariant_that the answer must be in the interval`[lo, hi]`. Let`mi = (lo + hi) / 2`. If`letters[mi] <= target`, then we must insert it in the interval`[mi + 1, hi]`. Otherwise, we must insert it in the interval`[lo, mi]`.

At the end, if our insertion position says to insert`target`into the last position`letters.length`, we return`letters[0]`instead. This is what the modulo operation does.

**Complexity Analysis**

* Time Complexity:O\(logN\)O\(logN\), whereNNis the length of`letters`. We peek only atlogNlogNelements in the array.

* Space Complexity:O\(1\)O\(1\), as we maintain only pointers.

```
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int lo = 0, hi = letters.length;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (letters[mi] <= target) lo = mi + 1;
            else hi = mi;
        }
        return letters[lo % letters.length];
    }
}
```



