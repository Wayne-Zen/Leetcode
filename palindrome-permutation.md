[Link](https://leetcode.com/problems/palindrome-permutation/)

```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        int[] freq = new int[256];
        for (char c : s.toCharArray()) {
            freq[c]++;
        }
        int odd = 0;
        for (int i = 0; i < freq.length; i++) {
            if(freq[i] % 2 == 1) {
                odd++;
            } 
        }
        if (s.length() % 2 == 0) {
            return odd == 0;
        } else {
            return odd == 1;
        }
    }
}
```
