[Link](https://leetcode.com/problems/plus-one/)

```java
public class Solution {
    public int[] plusOne(int[] digits) {
        int carry = 1;
        int n = digits.length;
        for (int i = n - 1; i >= 0; i--) {
            int sum = digits[i] + carry;
            digits[i] = sum % 10;
            carry = sum / 10;
        }
        if (carry == 1) {
            digits = new int[n + 1];
            digits[0] = 1;
            for (int i = 1; i < n + 1; i++) {
                digits[i] = 0;
            }
        }
        return digits;
    }
}
```
