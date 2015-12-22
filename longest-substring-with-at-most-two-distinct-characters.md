[Link](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        HashMap<Character, Integer> freq = new HashMap<Character, Integer>();
        int lo = -1; // exclusive
        int hi = -1;
        boolean expand = true;
        int max = 0;
        while (true) {
            if (expand) {
                hi++;
                if (hi == s.length()) {
                    break;
                }
                char c = s.charAt(hi);
                freq.put(c, freq.containsKey(c) ? freq.get(c) + 1 : 1);
                if (freq.size() > 2) {
                    expand = false;
                } else {
                    max = Math.max(max, hi - lo);
                }
            } else {
                lo++;
                char c = s.charAt(lo);
                freq.put(c, freq.get(c) - 1);
                if (freq.get(c) == 0) {
                    freq.remove(c);
                }
                if (freq.size() <= 2) {
                    expand = true;
                    max = Math.max(max, hi - lo);
                }
            }
        }
        return max;
    }
}
```
