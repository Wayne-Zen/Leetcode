[Link](https://leetcode.com/problems/reverse-words-in-a-string/)

```java
public class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        StringBuilder trim = new StringBuilder();
        char prev = ' ';
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == ' ') {
                if (prev != ' ') {
                    trim.append(' ');
                    prev = c;
                }
            } else {
                trim.append(c);
                prev = c;
            }
        }
        if (trim.length() != 0 && trim.charAt(trim.length() - 1) == ' ') {
            trim.deleteCharAt(trim.length() - 1);
        }
        s = trim.toString();

        char[] arr = new char[s.length()];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = s.charAt(i);
        }
        help(arr, 0, arr.length - 1);
        int lo = 0;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == ' ') {
                help(arr, lo, i - 1);
                lo = i + 1;
            }
        }
        help(arr, lo, arr.length - 1);
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < arr.length; i++) {
            sb.append(arr[i]);
        }
        return sb.toString();
    }
    private void help(char[] arr, int lo, int hi) {
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
