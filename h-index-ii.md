[Link](https://leetcode.com/problems/h-index-ii/)

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<List<String>>();
        // root string to group index
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        for (int i = 0; i < strs.length; i++) {
            char[] s_arr = strs[i].toCharArray();
            Arrays.sort(s_arr);
            String s = String.valueOf(s_arr);
            if (map.containsKey(s)) {
                res.get(map.get(s)).add(strs[i]);
            } else {
                map.put(s, map.size());
                List<String> sub = new ArrayList<String>();
                sub.add(strs[i]);
                res.add(sub);
            }
        }
        //sort result
        for (List<String> sub : res) {
            Collections.sort(sub);
        }
        return res;
    }
}
```

```java
public class Solution {
    public int hIndex(int[] citations) {
        int N = citations.length;
        for (int i = N - 1; i >= 0; i--) {
            if (citations[i] < N - i) {
                return N - i - 1;
            }
        }
        return N;
    }
}
```
