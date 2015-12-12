[Link](https://leetcode.com/problems/expression-add-operators/)

```java
public class Solution {
    
    public List<String> addOperators(String num, int target) {
        List<String> res = new ArrayList<String>();
        helper(res, num, target, "", 0, 0);
        return res;
    }
    
    private void helper(List<String> res, String num, int target, String tmp, long currRes, long prevNum){
        // 如果计算结果等于目标值，且所有数都用完了，则是有效结果
        if(currRes == target && num.length() == 0){
            String exp = new String(tmp);
            res.add(exp);
            return;
        }
        // 搜索所有可能的拆分情况
        for(int i = 1; i <= num.length(); i++){
            String currStr = num.substring(0, i);
            // 对于前导为0的数予以排除
            if(currStr.length() > 1 && currStr.charAt(0) == '0'){
                // 这里是return不是continue
                return;
            }
            // 得到当前截出的数
            long currNum = Long.parseLong(currStr);
            // 去掉当前的数，得到下一轮搜索用的字符串
            String next = num.substring(i);
            // 如果不是第一个字母时，可以加运算符，否则只加数字
            if(tmp.length() != 0){
                // 乘法
                helper(res, next, target, tmp+"*"+currNum, (currRes - prevNum) + prevNum * currNum, prevNum * currNum);
                // 加法
                helper(res, next, target, tmp+"+"+currNum, currRes + currNum, currNum);
                // 减法
                helper(res, next, target, tmp+"-"+currNum, currRes - currNum, -currNum); 
            } else {
                // 第一个数
                helper(res, next, target, currStr, currNum, currNum);
            }

        }
    }
}
```

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
