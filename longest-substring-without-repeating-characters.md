[Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

* 初始化 loc 为 －1
* 遍历end，如果上一次出现相同的c 在 star 之前，截取

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int max = 0;
        int start = 0;
        int[] loc = new int[256];
        for (int i = 0; i < loc.length; i++) {
            loc[i] = -1;
        }
        for (int end = 0; end < s.length(); end++) {
            char c = s.charAt(end);
            if (loc[c] >= start) {
                start = loc[c] + 1;
            }
            int len = end - start + 1;
            loc[c] = end;
            max = Math.max(max, len);
        }
        return max;
    }
}
```
