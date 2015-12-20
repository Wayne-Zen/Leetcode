[Link](https://leetcode.com/problems/word-pattern-ii/)

```java
public class Solution {
    public boolean wordPatternMatch(String pattern, String str) {
        HashMap<Character, String> map = new HashMap<Character, String>();
        HashSet<String> set = new HashSet<String>();
        return help(map, set, pattern, str);
    }
    
    private boolean help(HashMap<Character, String> map,
                         HashSet<String> set,
                         String pattern, String str) {
        if (pattern.length() == 0 && str.length() == 0) {
            return true;
        }
        if (pattern.length() == 0 || str.length() == 0) {
            return false;
        }
        char p = pattern.charAt(0);
        for (int i = 0; i < str.length(); i++) {
            String prefix = str.substring(0, i + 1);
            String suffix = str.substring(i + 1);
            if ((map.containsKey(p) && !map.get(p).equals(prefix)) 
                    || (!map.containsKey(p) && set.contains(prefix))) {
                    continue;
            }
            boolean insert = !map.containsKey(p);
            if (insert) {
                map.put(p, prefix);
                set.add(prefix);
            }
            if (help(map, set, pattern.substring(1), suffix)) {
                return true;
            }
            if (insert) {
                map.remove(p);
                set.remove(prefix);
            }
        }
        return false;
    }
}
```
