[Link](https://leetcode.com/problems/group-shifted-strings/)

```java
public class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        List<List<String>> res = new ArrayList<List<String>>();
        if (strings == null || strings.length == 0) {
            return res;
        }
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        for (String str : strings) {
            String key = convert(str);
            if (map.containsKey(key)) {
                map.get(key).add(str);
            } else {
                List<String> group = new ArrayList<String>();
                group.add(str);
                map.put(key, group);
            }
        }
        for (String key : map.keySet()) {
            Collections.sort(map.get(key));
            res.add(map.get(key));
        }
        return res;
    }
    private String convert(String str) {
        if (str.length() == 0) {
            return str;
        }
        int offset = str.charAt(0) - 'a';
        StringBuilder sb = new StringBuilder();
        sb.append('a');
        for (int i = 1; i < str.length(); i++) {
            char c = (char)(((str.charAt(i) - 'a' - offset) + 26) % 26 + 'a');
            sb.append(c);
        }
        return sb.toString();
    }
}
```
