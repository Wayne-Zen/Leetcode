[Link](https://leetcode.com/problems/minimum-window-substring/)

```java
public class Solution {
    public String minWindow(String s, String t) {
        int[] targetFreq = new int[256];
        int charNum = 0;
        for (char c : t.toCharArray()) {
            if (targetFreq[c] == 0) {
                charNum++;
            }
            targetFreq[c]++;
        }
        int lo = -1; // exclusive
        int hi = -1;
        boolean expand = true;
        int matchCnt = 0;
        int[] windowFreq = new int[256];
        int min = s.length() + 1;
        String res = "";
        while (true) {
            if (expand) {
                hi++;
                if (hi == s.length()) {
                    break;
                }
                char c = s.charAt(hi);
                windowFreq[c]++;
                if (windowFreq[c] == targetFreq[c]) {
                    matchCnt++;
                }
                if (matchCnt == charNum) {
                    expand = false;
                    if (hi - lo < min) {
                        min = hi - lo;
                        res = s.substring(lo + 1, hi + 1);
                    }
                }
            } else {
                lo++;
                char c = s.charAt(lo);
                windowFreq[c]--;
                if (windowFreq[c] < targetFreq[c]) {
                    matchCnt--;
                }
                if (matchCnt < charNum) {
                    expand = true;
                } else {
                    if (hi - lo < min) {
                        min = hi - lo;
                        res = s.substring(lo + 1, hi + 1);
                    }
                }
            }
        }
        return res;
    }
}
```
