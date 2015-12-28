[Link](https://leetcode.com/problems/multiply-strings/)

```java
public class Solution {
    public String multiply(String num1, String num2) {
        int[] res = new int[num1.length() + num2.length()];
        for (int i = 0; i < num1.length(); i++) {
            for (int j = 0; j < num2.length(); j++) {
                int num0 = num1.length() - 1 - i + num2.length() - 1 - j;
                int loc = res.length - num0 - 1;
                res[loc] += (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
            }
        }
        int carry = 0;
        for (int i = res.length - 1; i >= 0; i--) {
            int val = carry + res[i];
            res[i] = val % 10;
            carry = val / 10;
        }
        StringBuilder sb = new StringBuilder();
        int start = res.length - 1;
        for (int i = 0; i < res.length; i++) {
            if (res[i] != 0) {
                start = i; 
                break;
            }
        }
        for (int i = start; i < res.length; i++) {
            sb.append(res[i]);
        }
        return sb.toString();
    }
}
```
