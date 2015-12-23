[Link](https://leetcode.com/problems/anagrams/)

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        for (String str : strs) {
            char[] arr = str.toCharArray();
            Arrays.sort(arr);
            String s = String.valueOf(arr);
            if (map.containsKey(s)) {
                map.get(s).add(str);
            } else {
                List<String> group = new ArrayList<String>();
                group.add(str);
                map.put(s, group);
            }
        }
        List<List<String>> res = new ArrayList<List<String>>();
        for (List<String> group : map.values()) {
            Collections.sort(group);
            res.add(group);
        }
        return res;
    }
}
```
