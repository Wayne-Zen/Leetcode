[Link](https://leetcode.com/problems/generalized-abbreviation/)

```java
public class Solution {
    public List<String> generateAbbreviations(String word) {
        List<String> res = new ArrayList<String>();
        int N = word.length();
        for (int i = 0; i < (1 << N); i++) {
            // build word from i
            StringBuilder sb = new StringBuilder();
            int cnt = 0;
            for (int k = N - 1; k >= 0; k--) {
                if (((i >> k) & 1) == 1) {
                    cnt++;
                } else {
                    if (cnt != 0) {
                        sb.append(cnt);
                    }
                    sb.append(word.charAt(N - k - 1));
                    cnt = 0;
                }
            }
            if (cnt != 0) {
                sb.append(cnt);
            }
            res.add(sb.toString());
        }
        return res;
    }
}
```
