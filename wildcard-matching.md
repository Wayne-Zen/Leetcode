[Link](https://leetcode.com/problems/wildcard-matching/)

[https://www.zybuluo.com/wayne-zen/note/144290](https://www.zybuluo.com/wayne-zen/note/144290)

```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: A boolean
     */
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        
        int M = p.length() + 1;
        int N = s.length() + 1;
        boolean[][] f = new boolean[M][N];
        f[0][0] = true;
        
        // empty s can only match to allStar p
        boolean allStar = true;
        for (int i = 1; i < M; i++) {
            if (p.charAt(i - 1) != '*') {
                allStar = false;
            }
            f[i][0] = allStar ? true : false;
        }
        for (int j = 1; j < N; j++) {
            f[0][j] = false;
        }

        for (int i = 1; i < M; i++) {
            for (int j = 1; j < N; j++) {
                if (p.charAt(i - 1) == s.charAt(j - 1) 
                        || p.charAt(i - 1) == '?') {
                    f[i][j] = f[i - 1][j - 1];    
                } else if (p.charAt(i - 1) == '*') {
                    f[i][j] = f[i - 1][j] || f[i][j - 1];
                } else {
                    f[i][j] = false;
                }
            }
        }
        return f[M - 1][N - 1];
    }
}
```
