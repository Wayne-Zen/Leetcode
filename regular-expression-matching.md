[Link](https://leetcode.com/problems/regular-expression-matching/)

[https://www.zybuluo.com/wayne-zen/note/224226](https://www.zybuluo.com/wayne-zen/note/224226)

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
        
        // empty s can only match to all .* p
        for (int i = 2; i < M; i+=2) {
            if (p.charAt(i - 1) == '*') {
                f[i][0] = true;
            } else {
                break;
            }
        }

        for (int i = 1; i < M; i++) {
            for (int j = 1; j < N; j++) {
                if (p.charAt(i - 1) == s.charAt(j - 1) 
                        || p.charAt(i - 1) == '.') {
                    f[i][j] = f[i - 1][j - 1];    
                } else if (p.charAt(i - 1) == '*') {
                    if (p.charAt(i - 2) == s.charAt(j - 1) || p.charAt(i - 2) == '.') {
                        f[i][j] = f[i - 2][j] || f[i][j - 1];
                    } else {
                        f[i][j] = f[i - 2][j];
                    }
                }
            }
        }
        return f[M - 1][N - 1];
    }
}

```
