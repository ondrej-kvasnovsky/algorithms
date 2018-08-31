# Read N Characters Given Read4 II - Call multiple times

The API:`int read4(char *buf)`reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the`read4`API, implement the function`int read(char *buf, int n)`that readsncharacters from the file.

**Note:**  
The`read`function may be called multiple times.

**Example 1: **

```
Given buf = "abc"
read("abc", 1) // returns "a"
read("abc", 2); // returns "bc"
read("abc", 1); // returns ""
```

**Example 2: **

```
Given buf = "abc"
read("abc", 4) // returns "abc"
read("abc", 1); // returns ""
```

## Solution

```
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    public int read(char[] buf, int n) {
        
    }
}
```



