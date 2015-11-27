[Link](https://leetcode.com/problems/reverse-words-in-a-string/)

```java
public class Solution {
    public String reverseWords(String s) {
        boolean space = true;
        StringBuilder sb = new StringBuilder();
        List<String> ss = new ArrayList<String>();
        for (int i = 0; i <= s.length(); i++) {
            char c = i == s.length() ? ' ' : s.charAt(i);
            if (space && c == ' ') {
                space = true;
            } else if (space && c != ' ') {
                sb = new StringBuilder();
                sb.append(c);
                space = false;
            } else if (!space && c == ' ') {
                ss.add(sb.toString());
                space = true;
            } else if (!space && c != ' ') {
                sb.append(c);
                space = false;
            }
        }
        sb = new StringBuilder();
        for (int i = ss.size() - 1; i >= 0; i--) {
            if (i != ss.size() - 1) {
                sb.append(' ');
            }
            sb.append(ss.get(i));
        }
        return sb.toString();
    }
}
```
