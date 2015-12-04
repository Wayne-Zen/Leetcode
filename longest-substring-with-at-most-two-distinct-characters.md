[Link](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s == null || s.length() < 2) {
            return s.length();
        }
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int max = 0;
        int head = 0;
        int tail = 0;
        map.put(s.charAt(0), 1);
        boolean expand = true;
        while (head < s.length()) {
            if (expand) {
                if (head + 1 == s.length()) break;
                char c = s.charAt(head + 1);
                if (map.size() == 2) {
                    if (map.containsKey(c)) {
                        map.put(c, map.get(c) + 1);
                        head++;
                    } else {
                        expand = false;
                    }
                } else {
                    if (!map.containsKey(c)) {
                        map.put(c, 1);
                    } else {
                        map.put(c, map.get(c) + 1);
                    }
                    head++;
                }
            } else {
                char c = s.charAt(tail);
                if (map.get(c) == 1) {
                    map.remove(c);
                    expand = true;
                } else {
                    map.put(c, map.get(c) - 1);
                }
                tail++;
            }
            max = Math.max(max, head - tail + 1);
        }
        
        return max;
    }
}
```
