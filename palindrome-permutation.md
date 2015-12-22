[Link](https://leetcode.com/problems/palindrome-permutation/)

```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        int[] cnt = new int[256];
        for (char c : s.toCharArray()) {
            cnt[c]++;
        }
        int odd = 0;
        for (char c = 0; c < 256; c++) {
            if (cnt[c] % 2 == 1) {
                odd++;
            }
        }
        return s.length() % 2 == odd;
    }
}
```
