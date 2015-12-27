[Link](https://leetcode.com/problems/reverse-words-in-a-string/)

```java
public class Solution {
    public String reverseWords(String s) {
        s = " " + s + " ";
        s = reverse(s);
        StringBuilder sb = new StringBuilder();
        char prev = ' ';
        StringBuilder res = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (c == ' ') {
                if (prev != ' ') {
                    String token = sb.toString();
                    sb = new StringBuilder();
                    res.append((res.length() == 0 ? "" : " ") + reverse(token));
                }
            } else {
                sb.append(c);
            }
            prev = c;
        }
        return res.toString();
    }
    private String reverse(String s) {
        int lo = 0;
        int hi = s.length() - 1;
        char[] arr = s.toCharArray();
        while (lo < hi) {
            char temp = arr[lo];
            arr[lo] = arr[hi];
            arr[hi] = temp;
            lo++;
            hi--;
        }
        return String.valueOf(arr);
    }
}
```
