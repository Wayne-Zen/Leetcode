[Link](https://leetcode.com/problems/word-pattern/)

```java
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        HashMap<Character, String> map = new HashMap<Character, String>();
        HashMap<String, Character> map2 = new HashMap<String, Character>();
        String[] ss = str.split("\\s");
        if (ss.length != pattern.length()) {
            return false;
        }
        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern.charAt(i);
            if (!map.containsKey(c)) {
                map.put(c, ss[i]);
            } else {
                if (!map.get(c).equals(ss[i])) {
                    return false;
                }
            }
            if (!map2.containsKey(ss[i])) {
                map2.put(ss[i], c);
            } else {
                if (map2.get(ss[i]) != c) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
