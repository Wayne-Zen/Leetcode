[Link](https://leetcode.com/problems/word-pattern-ii/)

```java
public class Solution {
    public boolean wordPatternMatch(String pattern, String str) {
        HashMap<Character, String> map1 = new HashMap<Character, String>();
        HashMap<String, Character> map2 = new HashMap<String, Character>();
        return help(map1, map2, pattern, str);
    }
    
    private boolean help(HashMap<Character, String> map1,
                         HashMap<String, Character> map2,
                         String pattern, String str) {
        if (pattern.length() == 0 && str.length() == 0) {
            return true;
        }
        if (pattern.length() == 0 || str.length() == 0) {
            return false;
        }
        char p = pattern.charAt(0);
        for (int i = 0; i < str.length(); i++) {
            String sub1 = str.substring(0, i + 1);
            String sub2 = str.substring(i + 1);
            boolean remove1 = false;
            boolean remove2 = false;
            if (map1.containsKey(p)) {
                remove1 = false;
                if (!map1.get(p).equals(sub1)) {
                    continue;
                }
            } else {
                remove1 = true;
                map1.put(p, sub1);
            }
            if (map2.containsKey(sub1)) {
                remove2 = false;
                if (!map2.get(sub1).equals(p)) {
                    // 坑！！， 第一个字典通过，第二个字典没通过，要记得撤销第一个字典的最近操作
                    if (remove1) {
                        map1.remove(p);
                    }
                    continue;
                }
            } else {
                remove2 = true;
                map2.put(sub1, p);
            }
            if (help(map1, map2, pattern.substring(1), sub2)) {
                return true;
            }
            if (remove1) {
                map1.remove(p);
            }
            if (remove2) {
                map2.remove(sub1);
            }
        }
        return false;
    }
}
```
