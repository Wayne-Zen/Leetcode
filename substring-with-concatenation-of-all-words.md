[Link](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

* 新建HashMap，注意判断
* words 可能有duplicates

```java
public class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<Integer>();
        HashMap<String, Integer> frequency = new HashMap<String, Integer>();
        for (int i = 0; i < words.length; i++) {
            if (frequency.containsKey(words[i])) {
                frequency.put(words[i], frequency.get(words[i]) + 1);
            } else {
                frequency.put(words[i], 1);
            }
        }
        int len = words[0].length();
        int total_len = len * words.length;
        for (int i = 0; i < s.length() - total_len + 1; i++) {
            HashMap<String, Integer> localFrequency = new HashMap<String, Integer>();
            int j = 0;
            for (; j < total_len; j += len) {
                String token = s.substring(i + j, i + j + len);
                if (!frequency.containsKey(token)) {
                    break;
                } else {
                    if (localFrequency.containsKey(token)) {
                        int cnt = localFrequency.get(token) + 1;
                        if (cnt > frequency.get(token)) {
                            break;
                        }
                        localFrequency.put(token, cnt);
                    } else {
                        localFrequency.put(token, 1);
                    }
                }
            }
            if (j == total_len) {
                res.add(i);
            }
        }
        
        return res;
    }
}
```
