[Link](https://leetcode.com/problems/additive-number/)

```java
import java.math.*;

public class Solution {
    public boolean isAdditiveNumber(String num) {
        if (num == null || num.length() < 3) {
            return false;
        }
        int bound = num.length() / 3 * 2 + 1;
        for (int i = 1; i <= bound; i++) {
            if (num.charAt(0) == '0' && i != 1) { // 坑
                continue;
            }
            String s1 = num.substring(0, i);
            for (int j = 1; i + j <= bound; j++) {
                if (num.charAt(i) == '0' && j != 1) { // 坑
                    continue;
                }
                String s2 = num.substring(i, i + j);
                if (check(num, s1, s2)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    private boolean check(String num, String s1, String s2) {
        StringBuilder sb = new StringBuilder();
        sb.append(s1);
        sb.append(s2);
        // 坑, 至少要加一次
        do {
            BigInteger v1 = new BigInteger(s1);
            BigInteger v2 = new BigInteger(s2);
            BigInteger v = v1.add(v2);
            s1 = s2;
            s2 = v.toString();
            sb.append(s2);
        } while (sb.length() < num.length());
        return num.equals(sb.toString());
    }
}
```
