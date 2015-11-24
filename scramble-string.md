[Link](https://leetcode.com/problems/scramble-string/)

* 注意层次的安排
* 注意 i，j 需要逆序遍历
* i，j 的范围根据k变化


<img scr="img/Photos/scramble-string.jpg" width="500">

```java
public class Solution {
    // dp[k][i][j]表示 从s1[i], s2[j]起始, 长度为k的串是否是重组字符串
    // i,j ~ [0, len - 1]
    // k ~ [1, len]
    public boolean isScramble(String s1, String s2) {
        int len = s1.length();
        if (len != s2.length()) {
            return false;
        }
        if (len == 0) {
            return true;
        }
        
        boolean[][][] dp = new boolean[len + 1][len][len];
        for(int i = 0; i < len; i++){
            for(int j = 0; j < len; j++){
                dp[1][i][j] = (s1.charAt(i) == s2.charAt(j)); // k==1
            }
        }
        
        for (int k = 2; k <= len; k++) {
            for (int i = len - k; i >= 0; i--) {
                for (int j = len - k; j >= 0; j--) {
                    boolean res = false;
                    for (int m = 1; m < k; m++) {
                        if ((dp[m][i][j] && dp[k - m][i + m][j + m]) 
                                || (dp[m][i][j + k - m] && dp[k - m][i + m][j])) {
                            res = true;
                            break;
                        }
                    }
                    dp[k][i][j] = res;
                }
            }
        }
        
        return dp[len][0][0];
    }
}
```
