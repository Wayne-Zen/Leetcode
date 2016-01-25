[Link](https://leetcode.com/problems/word-pattern-ii/)

```java
public class Solution {
    public boolean wordPatternMatch(String pattern, String str) {
        HashMap<Character, String> map = new HashMap<Character, String>();
        HashSet<String> set = new HashSet<String>();
        return help(map, set, pattern, str);
    }
    private boolean help(HashMap<Character, String> map, HashSet<String> set, String pattern, String str) {
        if (pattern.length() == 0) {
            return str.length() == 0;
        }
        char c = pattern.charAt(0);
        for (int i = 0; i < str.length(); i++) {
            String prefix = str.substring(0, i + 1);
            String suffix = str.substring(i + 1);
            boolean insert = false;
            if (map.containsKey(c)) {
                if (!map.get(c).equals(prefix)) {
                    continue;
                }
            } else {
                if (set.contains(prefix)) {
                    continue;
                } else {
                    insert = true;
                    map.put(c, prefix);
                    set.add(prefix);
                }
            }
            if (help(map, set, pattern.substring(1), suffix)) {
                return true;
            }
            if (insert) {
                map.remove(c);
                set.remove(prefix);
            }
        }
        return false;
    }
}
```
