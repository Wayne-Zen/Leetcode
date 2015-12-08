[Link](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s == null || s.length() < 2) {
            return s.length();
        }
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int max = 0;
        int lo = -1; // exclusive
        int hi = -1;
        boolean expand = true;
        while (true) {
            if (expand) {
                hi++;
                if (hi == s.length()) {
                    break;
                }
                char c = s.charAt(hi);
                if (!map.containsKey(c)) {
                    map.put(c, 1);
                } else {
                    map.put(c, map.get(c) + 1);
                }
                if (map.size() <= 2) {
                    max = Math.max(max, hi - lo);
                } else {
                    expand = false;
                }
            } else {
                lo++;
                char c = s.charAt(lo);
                map.put(c, map.get(c) - 1);
                if (map.get(c) == 0) {
                    map.remove(c);
                    expand = true;
                }
            }
        }
        
        return max;
    }
}
```
