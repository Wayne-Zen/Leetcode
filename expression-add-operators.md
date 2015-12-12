[Link](https://leetcode.com/problems/expression-add-operators/)


```java
public class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> res = new ArrayList<String>();
        if (num == null || num.length() == 0) {
            return res;
        }
        for (int i = 0; i < num.length(); i++) {
            String token = num.substring(0, i + 1);
            long val = Long.valueOf(token);
            String rest = num.substring(i + 1);
            if (token.length() != 1 && token.charAt(0) == '0') {
                continue;
            }
            help(res, token, rest, target, val, val);
        }
        return res;
    }
    
    private void help(List<String> res, String now, String num,
                      int target, long sum, long preVal) {
        if (num.length() == 0 && target == sum) {
            res.add(now);
            return;
        }
        for (int i = 0; i < num.length(); i++) {
            String token = num.substring(0, i + 1);
            long val = Long.valueOf(token);
            String rest = num.substring(i + 1);
            if (token.length() != 1 && token.charAt(0) == '0') {
                continue;
            }
            help(res, now + '+' + token, rest, target, sum + val, val);
            help(res, now + '-' + token, rest, target, sum - val, -val);
            help(res, now + '*' + token, rest, target, (sum - preVal) + preVal * val, preVal * val);
        }
    }
}
```
