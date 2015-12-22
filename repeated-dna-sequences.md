[Link](https://leetcode.com/problems/repeated-dna-sequences/)

```java
public class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        for (int i = 0; i <= s.length() - 10; i++) {
            String token = s.substring(i, i + 10);
            if (!map.containsKey(token)) {
                map.put(token, 1);
            } else {
                map.put(token, map.get(token) + 1);
            }
        }
        List<String> res = new ArrayList<String>();
        for (String token : map.keySet()) {
            if (map.get(token) > 1) {
                res.add(token);
            }
        }
        return res;
    }   
}
```

```java
public class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> res = new ArrayList<String>();
        if (s == null || s.length() <= 10) {
            return res;
        }
        int[] table = new int[256];
        table['C'] = 1;
        table['G'] = 2;
        table['T'] = 3;
        int[] cnt = new int[1024 * 1024];
        int index = 0;
        for (int i = 0; i < 10; i++) {
            index += table[s.charAt(i)] << (2 * i);
        }
        cnt[index]++;
        for (int i = 10; i < s.length(); i++) {
            index >>= 2;
            index += table[s.charAt(i)] << (2 * 9);
            if (cnt[index] == 1) {
                res.add(s.substring(i - 9, i + 1));
            }
            cnt[index]++;
        }
        return res;
    }   
}
```
