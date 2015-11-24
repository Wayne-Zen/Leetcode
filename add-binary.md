[Link](https://leetcode.com/problems/add-binary/)


```java
public class Solution {
    public String addBinary(String a, String b) {
        int carry = 0;
        StringBuilder sb = new StringBuilder();
        if (a.length() > b.length()) {
            String temp = a;
            a = b;
            b = temp;
        }
        // l1 <= l2
        int l1 = a.length();
        int l2 = b.length();
        for (int i = 0; i < l1; i++) {
             int c1 = a.charAt(l1 - 1 - i) - '0';
             int c2 = b.charAt(l2 - 1 - i) - '0';
             int sum = c1 + c2 + carry;
             int bit = sum % 2;
             carry = sum / 2;
             sb.append(bit);
        }
        for (int i = l1; i < l2; i++) {
            int c = b.charAt(l2 - 1 - i) - '0';
            int sum = c + carry;
            int bit = sum % 2;
            carry = sum / 2;
            sb.append(bit);
        }
        if (carry == 1) {
            sb.append(1);
        }
        return sb.reverse().toString();
    }
}
```
