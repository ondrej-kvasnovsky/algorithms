# Find the Duplicate Number

Given an array nums containing n+ 1 integers where each integer is between 1 and n \(inclusive\), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example 1:**

```
Input: [1,3,4,2,2]
Output: 2
```

**Example 2:**

```
Input: [3,1,3,4,2]
Output: 3
```

**Note:**

1. You **must not **modify the array \(assume the array is read only\).
2. You must use only constant, O\(1\) extra space.
3. Your runtime complexity should be less than _O_\(_n_2\).
4. There is only one duplicate number in the array, but it could be repeated more than once.

## Solution

#### Note {#note}

The first two approaches mentioned do not satisfy the constraints given in the prompt, but they are solutions that you might be likely to come up with during a technical interview. As an interviewer, I personally would_not_expect someone to come up with the cycle detection solution unless they have heard it before.

#### Proof {#proof}

Proving that at least one duplicate must exist in`nums`is simple application of the[pigeonhole principle](https://en.wikipedia.org/wiki/Pigeonhole_principle). Here, each number in`nums`is a "pigeon" and each distinct number that can appear in`nums`is a "pigeonhole". Because there aren+1n+1numbers arenndistinct possible numbers, the pigeonhole principle implies that at least one of the numbers is duplicated.

#### Approach \#1 Sorting \[Accepted\] {#approach-1-sorting-accepted}

**Intuition**

If the numbers are sorted, then any duplicate numbers will be adjacent in the sorted array.

**Algorithm**

Given the intuition, the algorithm follows fairly simply. First, we sort the array, and then we compare each element to the previous element. Because there is exactly one duplicated element in the array, we know that the array is of at least length 2, and we can return the duplicate element as soon as we find it.

**Complexity Analysis**

* Time complexity :O\(nlgn\)O\(nlgn\)

  The`sort`invocation costsO\(nlgn\)O\(nlgn\)time in Python and Java, so it dominates the subsequent linear scan.

* Space complexity :O\(1\)O\(1\)\(orO\(n\)O\(n\)\)

  Here, we sort`nums`in place, so the memory footprint is constant. If we cannot modify the input array, then we must allocate linear space for a copy of`nums`and sort that instead.

```
class Solution {
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i-1]) {
                return nums[i];
            }
        }

        return -1;
    }
}
```

---

#### Approach \#2 Set \[Accepted\] {#approach-2-set-accepted}

**Intuition**

If we store each element as we iterate over the array, we can simply check each element as we iterate over the array.

**Algorithm**

In order to achieve linear time complexity, we need to be able to insert elements into a data structure \(and look them up\) in constant time. A`Set`satisfies these constraints nicely, so we iterate over the array and insert each element into`seen`. Before inserting it, we check whether it is already there. If it is, then we found our duplicate, so we return it.

**Complexity Analysis**

* Time complexity :O\(n\)O\(n\)

  `Set`in both Python and Java rely on underlying hash tables, so insertion and lookup have amortized constant time complexities. The algorithm is therefore linear, as it consists of a`for`loop that performs constant worknntimes.

* Space complexity :O\(n\)O\(n\)

  In the worst case, the duplicate element appears twice, with one of its appearances at array indexn−1n−1. In this case,`seen`will containn−1n−1distinct values, and will therefore occupyO\(n\)O\(n\)space.

```
class Solution {
    public int findDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<Integer>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return num;
            }
            seen.add(num);
        }

        return -1;
    }
}
```

---

#### Approach \#3 Floyd's Tortoise and Hare \(Cycle Detection\) \[Accepted\] {#approach-3-floyds-tortoise-and-hare-cycle-detection-accepted}

**Intuition**

If we interpret`nums`such that for each pair of indexiiand valueviv​i​​, the "next" valuevjv​j​​is at indexviv​i​​, we can reduce this problem to cycle detection. See the solution to[Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/solution/)for more details.

**Algorithm**

First off, we can easily show that the constraints of the problem imply that a cycle_must_exist. Because each number in`nums`is between11andnn, it will necessarily point to an index that exists. Therefore, the list can be traversed infinitely, which implies that there is a cycle. Additionally, because00cannot appear as a value in`nums`,`nums[0]`cannot be part of the cycle. Therefore, traversing the array in this manner from`nums[0]`is equivalent to traversing a cyclic linked list. Given this, the problem can be solved just like[Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/).

To see the algorithm in action, check out the animation below:

1 / 25

**Complexity Analysis**

* Time complexity :O\(n\)O\(n\)

  For detailed analysis, refer to[Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/solution/#approach-2-floyds-tortoise-and-hare-accepted).

* Space complexity :O\(1\)O\(1\)

  For detailed analysis, refer to[Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/solution/#approach-2-floyds-tortoise-and-hare-accepted).

```
class Solution {
    public int findDuplicate(int[] nums) {
        // Find the intersection point of the two runners.
        int tortoise = nums[0];
        int hare = nums[0];
        do {
            tortoise = nums[tortoise];
            hare = nums[nums[hare]];
        } while (tortoise != hare);

        // Find the "entrance" to the cycle.
        int ptr1 = nums[0];
        int ptr2 = tortoise;
        while (ptr1 != ptr2) {
            ptr1 = nums[ptr1];
            ptr2 = nums[ptr2];
        }

        return ptr1;
    }
}
```



