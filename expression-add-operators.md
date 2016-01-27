[Link](https://leetcode.com/problems/expression-add-operators/)


```java

public class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> res = new ArrayList<String>();
        if (num == null || num.length() == 0) {
            return res;
        }
        help(res, "", 0, 0, num, target);
        return res;
    }
    private void help(List<String> res, String now, long sum, long preVal, String num, int target) {
        if (num.length() == 0) {
            if (sum == target) {
                res.add(now);
            }
            return;
        }
        for (int k = 0; k < num.length(); k++) {
            String prefix = num.substring(0, k + 1);
            String suffix = num.substring(k + 1);
            if (prefix.length() > 1 && prefix.charAt(0) == '0') {
                continue;
            }
            long curVal = Long.valueOf(prefix);
            if (now.length() == 0) {
                help(res, prefix, curVal, curVal, suffix, target);
            } else {
                help(res, now + "*" + prefix, sum - preVal + preVal * curVal, preVal * curVal, suffix, target);
                help(res, now + "+" + prefix, sum + curVal, curVal, suffix, target);
                help(res, now + "-" + prefix, sum - curVal, -curVal, suffix, target);
            }
        }
    }
}
```
