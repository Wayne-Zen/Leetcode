[Link](https://leetcode.com/problems/longest-valid-parentheses/)

* f[i]: 以s[i-1]结尾的longest valid parentheses substring的长度

<img src="https://lh3.googleusercontent.com/jtD-J8IM9b4gFnjW_mt4R1PJqUMcJzQ-klebDYixwhntNqIrMqBYm7WfojjpEF-b0grQEoJOqtyPtSvGFAOwurIFiFbR-hcKcMhuqNPR2vPyLQ2ZVdAIvtamRNtqK-m7Zh5XQscGWzswFhJZhkhubj4yz8z8vJY8ddgxK0TDyMCD76YSRllFg0yqmTW5hQ4VZTspAE7zSrTxZbTyGX4FBEBuExqgyNWF8uSE3vx_zQHdghh6OrIkArzal9HRrTZa8B6onIYTvDSBcKJpsKcXJ-BdheWOdCwEgA6KRL1BzQEru_D1cW5TAa2BCOTOxMf3Ond0RgAGGQ7vFfSAd1clGMRDIMutwcV1XSWVNTL_ajaAhNKsVralaWEZ8Ul6n8wCe46pKRP4OnTrDBTvae7s9uzMNAZbU1tAKMLeepeM2n1boR1YCkKpQqteclECAbYTUoYx-FfsUHOMNO1a2oN6B-EjxmlGp-Q-g-KrtTeqi6C7aN2UWzwh0yfT2DHH2epD--T0D1JyoRCjUq1p_m0qdckQudPikDJ4gyVRLlKv6hg=w1235-h927-no" width="300">
  
  
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
