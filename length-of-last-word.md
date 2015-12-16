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
```java
public class Solution {
    public int lengthOfLastWord(String s) {
        char prev = ' ';
        int start = -1;
        int len = 0;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == ' ') {
                if (prev != ' ') {
                    prev = c;
                    len = i - start;
                }
            } else {
                if (prev == ' ') {
                    prev = c;
                    start = i;
                }
            }
        }
        if (prev != ' ') {
            len = s.length() - start;
        }
        return len;
    }
}
```
