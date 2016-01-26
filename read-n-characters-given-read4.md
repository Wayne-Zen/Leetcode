[Link](https://leetcode.com/problems/read-n-characters-given-read4/)

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    public int read(char[] buf, int n) {
        char[] temp = new char[4];
        int index = 0;
        while (true) {
            int n4 = read4(temp);
            int copyNum = Math.min(n4, n - index);
            for (int i = 0; i < copyNum; i++) {
                buf[index++] = temp[i];
            }
            if (n4 < 4 || index == n) {
                return index;
            }
        }
    }
}
```
