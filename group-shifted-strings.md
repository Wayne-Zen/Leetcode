[Link](https://leetcode.com/problems/group-shifted-strings/)

```java
public class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        for (String s : strings) {
            String shift = shift(s);
            if (map.containsKey(shift)) {
                map.get(shift).add(s);
            } else {
                List<String> group = new ArrayList<String>();
                group.add(s);
                map.put(shift, group);
            }
        }
        List<List<String>> res = new ArrayList<List<String>>();
        for (List<String> group : map.values()) {
            Collections.sort(group);
            res.add(group);
        }
        return res;
    }
    private String shift(String s) {
        if (s.length() == 0) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        // c = 'a' + offset;
        sb.append('a');
        int offset = s.charAt(0) - 'a';
        for (int i = 1; i < s.length(); i++) {
            char c = s.charAt(i);
            char x = (char)(c - offset);
            if (x < 'a') {
                x += 26;
            } else if (x > 'z') {
                x -= 26;
            }
            sb.append(x);
        }
        System.out.println(sb.toString());
        return sb.toString();
    }
}
```
