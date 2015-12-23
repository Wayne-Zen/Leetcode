[Link](https://leetcode.com/problems/strobogrammatic-number-iii/)

```java
public class Solution {
    public int strobogrammaticInRange(String low, String high) {
        int loLen = low.length();
        int hiLen = high.length();
        int cnt = 0;
        for (int i = loLen; i <= hiLen; i++) {
            if (i == loLen || i == hiLen) {
                for (String s : getList(i)) {
                    if ((i == loLen && s.compareTo(low) < 0) 
                            || (i == hiLen && s.compareTo(high) > 0)) {
                        continue;
                    }
                    cnt++;
                }
            } else {
                cnt += count(i);
            }
        }
        return cnt;
    }
    /* 
     * For the first pair, we have 4 candidates: 1, 8, 6, 9 (excludes 0);
     * For every pair, we have 5 candidates: 0, 1, 8, 6, 9 ; 
     * For the mid of odd length, we have 3 candidates: 0, 1, 8.
     */
    private int count(int len) {
        if (len == 0) {
            return 0;
        }
        if (len == 1) {
            return 3;
        }
        if (len % 2 == 0) {
            return 4 * (int)Math.pow(5, len / 2 - 1);
        } else {
            return 4 * 3 * (int)Math.pow(5, len / 2 - 1);
        }
    }
    private List<String> getList(int len) {
        List<String> res = new ArrayList<String>();
        int n = len % 2;
        if (n == 1) {
            res.add("0");
            res.add("1");
            res.add("8");
        } else {
            res.add("");
        }
        while (n != len) {
            List<String> newRes = new ArrayList<String>();
            for (String s : res) {
                if (n + 2 != len) {
                    newRes.add("0" + s + "0");
                }
                newRes.add("1" + s + "1");
                newRes.add("8" + s + "8");
                newRes.add("6" + s + "9");
                newRes.add("9" + s + "6");
            }
            res = newRes;
            n += 2;
        }
        return res;
    }
}
```
