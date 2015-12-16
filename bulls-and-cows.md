[Link](https://leetcode.com/problems/bulls-and-cows/)

```java
public class Solution {
    public String getHint(String secret, String guess) {
        // val : cnt
        int[] cnt1 = new int[256];
        int[] cnt2 = new int[256];
        int bull = 0;
        for (int i = 0; i < secret.length(); i++) {
            char c1 = secret.charAt(i);
            char c2 = guess.charAt(i);
            if (c1 == c2) {
                bull++;
            } else {
                cnt1[c1]++;
                cnt2[c2]++;
            }
        }
        int cow = 0;
        for (char c = 0; c < 256; c++) {
            cow += Math.min(cnt1[c], cnt2[c]);
        }
        return bull + "A" + cow + "B";
    }
}
```
