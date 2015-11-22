[Link](https://leetcode.com/problems/regular-expression-matching/)

[https://www.zybuluo.com/wayne-zen/note/224226](https://www.zybuluo.com/wayne-zen/note/224226)

<img src="https://lh3.googleusercontent.com/949FvRr_BTm2eFSpzjjzmBvQiSUJF6DXAU6pggDSrhpg710UWUGvPawd8TVxAG0C2AxBXQtipp2MoGUAGk3LBwaJlyOlSMhETRSbq-mk0tB3jFwQtCy0AWq-e6Ib11e0qnhi6Tv10N9z5QZXGRbZeFSbQv9xQFWRRot-_hYshEes6dA0rn2ubt686EAsEjmn5p05SKgB7AGoaRtarp9p_YLaF9iZCJfhTH6Qmx4kjSlka_z766cV0PbXYKKb3wMAjBAJmNAQavCwp5OJlKE2aOLRzPQBuTTqiAmiYM7NDzds2Ic_zROip7tx_7KW83voveJLI-6-NKssyeXaMly5PgT1th_tSWmHUOjCDLiROryHknCGsQwqmo5DA5mz0cH31kv3MwK99wkoZud728Kcnv5zX_ztEVkJqwhAyXW7uCXhPVUaRzqV49Hax_jm5NmMn1_S--fqB8x3QJHZVpFJ4rdsuWIUEJVYvveWEvMSuDOCNPdM3QfpATFA1wpjnN41Jlpp0lx-cDt9ISds3_yAvsStV_kpgh0eLWgOHtwaTaA=w989-h1318-no" width="200">

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
