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
        char[] tmp=new char[4];
        int index=0;
        while(index<n){
            int len=read4(tmp);
            int  tmpIndex=0;
            while(index<n&&tmpIndex<len){
                buf[index++]=tmp[tmpIndex++];
            }
            if(len<4) return index;
        }
        return index;
    }
}
```
