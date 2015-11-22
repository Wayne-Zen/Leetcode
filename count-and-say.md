[Link](https://leetcode.com/problems/count-and-say/)

* 理解题意

```java
public class Solution {
    public String countAndSay(int n) {
        if (n == 1) {
            return "1";
        }
        String str = "1";
        for (int i = 1; i < n; i++) {   
            str = help(str);
        }    
        return str;
    }
    
    public String help(String str) {
        int cnt = 1;
        char c = str.charAt(0);
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i < str.length(); i++) {
            if (str.charAt(i) == c) {
                cnt++;
            } else {
                sb.append(String.valueOf(cnt));
                sb.append(c);
                cnt = 1;
                c = str.charAt(i);
            }
        }
        sb.append(String.valueOf(cnt));
        sb.append(c);
        return sb.toString();
    }
}
```
