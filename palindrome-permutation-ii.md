[Link](https://leetcode.com/problems/palindrome-permutation-ii/)

```java
public class Solution {
    public List<String> generatePalindromes(String s) {
        List<String> res = new ArrayList<String>();
        if (s == null || s.length() == 0) {
            return res;
        }
        int[] cnt = new int[256];
        for (char c : s.toCharArray()) {
            cnt[c]++;
        }
        int odd = 0;
        String oddc = "";
        for (char c = 0; c < 256; c++) {
            if (cnt[c] % 2 != 0) {
                odd++;
                oddc = String.valueOf(c);
            }
        }
        if (s.length() % 2 != odd) {
            return res;
        }
        
        int avail = 0;
        for (char c = 0; c < 256; c++) {
            cnt[c] /= 2;
            avail += cnt[c];
        }
        help(res, "", avail, cnt, oddc);
        return res;
    }
    
    private void help(List<String> res, String now, int avail,
                      int[] cnt, String oddc) {
        if (avail == 0) {
            StringBuilder rev = (new StringBuilder(now)).reverse();
            res.add(now + oddc + rev);
            return;
        }
        for (char c = 0; c < 256; c++) {
            if (cnt[c] == 0) {
                continue;
            }
            cnt[c]--;
            help(res, now + c, avail - 1, cnt, oddc);
            cnt[c]++;
        }
    }
}
```
