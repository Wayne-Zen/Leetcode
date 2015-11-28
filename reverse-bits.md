[Link](https://leetcode.com/problems/reverse-bits/)

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
    	for (int i = 0; i < 16; i++) {
    		n = swapBits(n, i, 32 - i - 1);
    	}
     
    	return n;
    }
     
    public int swapBits(int n, int i, int j) {
    	int a = (n >> i) & 1;
    	int b = (n >> j) & 1;
        // 如果 i j 相同，什么都不做
        // 如果 i j 不同，各自flip
    	if ((a ^ b) != 0) {
    		return n ^= (1 << i) | (1 << j);
    	}
     
    	return n;
    }
}
```
