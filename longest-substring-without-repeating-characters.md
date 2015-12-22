[Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/)


```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        int lo = -1; // exclusive
        int hi = -1;
        boolean expand = true;
        int max = 0;
        int[] cnt = new int[256];
        char bump = ' ';
        while (true) {
            if (expand) {
                hi++;
                if (hi == s.length()) {
                    break;
                }
                char c = s.charAt(hi);
                cnt[c]++;
                if (cnt[c] > 1) {
                    expand = false;
                    bump = c;
                } else {
                    max = Math.max(max, hi - lo);
                }
            } else {
                lo++;
                char c = s.charAt(lo);
                cnt[c]--;
                if (bump == c && cnt[c] <= 1) {
                    expand = true;
                    bump = ' ';
                    max = Math.max(max, hi - lo);
                }
            }
        }
        return max;
    }
}
```
