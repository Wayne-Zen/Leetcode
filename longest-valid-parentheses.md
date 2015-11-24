[Link](https://leetcode.com/problems/longest-valid-parentheses/)

* f[i]: 以s[i-1]结尾的longest valid parentheses substring的长度

<img src="img/Photos/longest-valid-parentheses.png" width="400">
  
  
  ```java
  public class Solution {
    public int longestValidParentheses(String s) {
        int[] f = new int[s.length() + 1];
        int max = 0;
        f[0] = 0;
        // f[i] -> s[i - 1]
        for (int i = 1; i < f.length; i++) {
            if (s.charAt(i - 1) == '(') {
                f[i] = 0;
            } else { // ')'
                int j = i - 1 - f[i - 1];
                if (j - 1 >= 0 && s.charAt(j - 1) == '(') {
                    f[i] = f[i - 1] + 2 + f[j - 1];
                } else {
                    f[i] = 0;
                }
            }
            max = Math.max(max, f[i]);
        }
        
        return max;
    }
}
  ```
