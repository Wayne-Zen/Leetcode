[Link](https://leetcode.com/problems/length-of-last-word/)


```java
public class Solution {
    public int lengthOfLastWord(String s) {
        int res = 0;
        boolean space = true;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                space = true;
            } else {
                if (space) {
                    res = 1;
                    space = false;
                } else {
                    res++;
                }
            }
        }
        return res;
    }
}
```
