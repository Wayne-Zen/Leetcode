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
        while (index < n) {
            int n4 = read4(temp);
            for (int i = 0; i < n4; i++) {
                if (index < n) {
                    buf[index] = temp[i];
                    index++;
                } else {
                    return index;
                }
            }
            if (n4 < 4) {
                return index;
            }
        }
        return index;
    }
}
```
