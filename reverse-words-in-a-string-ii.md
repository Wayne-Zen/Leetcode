[Link](https://leetcode.com/problems/reverse-words-in-a-string-ii/)

```java
public class Solution {
    public void reverseWords(char[] s) {
        reverse(s, 0, s.length - 1);
        int lo = 0;
        for (int i = 0; i < s.length; i++) {
            if (s[i] == ' ') {
                reverse(s, lo, i - 1);
                lo = i + 1;
            }
        }
        reverse(s, lo, s.length -1);
    }
    
    private void reverse(char[] arr, int lo, int hi) {
        while (lo < hi) {
            char temp = arr[lo];
            arr[lo] = arr[hi];
            arr[hi] = temp;
            lo++;
            hi--;
        }
    }
}
```
