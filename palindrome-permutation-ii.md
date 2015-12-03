[Link](https://leetcode.com/problems/palindrome-permutation-ii/)

```java
public class Solution {
    public List<String> generatePalindromes(String s) {
        List<String> res = new ArrayList<String>();
        int[] freq = new int[256];
        for (char c : s.toCharArray()) {
            freq[c]++;
        }
        String odd = "";
        int oddCnt = 0;
        for (char c = 0; c < 256; c++) {
            if (freq[c] % 2 == 1) {
                if (oddCnt != 0) {
                    return res;
                }
                oddCnt++;
                odd = "" + c;
            }
        }
        if (s.length() % 2 == 0) {
            if (oddCnt != 0) {
                return res;
            } 
        } else {
            if (oddCnt != 1) {
                return res;
            }
        }
        int avail = 0;
        for (char c = 0; c < 256; c++) {
            freq[c] /= 2;
            avail += freq[c];
        }
        help(res, "", avail, freq, odd);
        return res;
    }
    
    private void help(List<String> res, String now,
                      int avail, int[] freq, String odd) {
        if (avail == 0) {
            StringBuilder sb = new StringBuilder(now);
            res.add(now + odd + sb.reverse().toString());
            return;
        }
        for (char c = 0; c < 256; c++) {
            if (freq[c] == 0) {
                continue;
            }
            freq[c]--;
            help(res, now + c, avail - 1, freq, odd);
            freq[c]++;
        }
    }
}
```
