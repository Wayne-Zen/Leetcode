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
        if (num == null ||  num.length() == 0) {
            return res;
        }
        help(res, "", num, target, 0);
        return res;
    }
    
    private void help(List<String> res, 
                      String now, String num,
                      long target, long preVal) {
        if (target == 0 && num.length() == 0) {
            res.add(now);
            return;
        }
        for (int i = 0; i < num.length(); i++) {
            String sub = num.substring(0, i + 1);
            String rest = num.substring(i + 1);
            if (sub.length() > 1 && sub.charAt(0) == '0') {
                return;
            }
            long curVal = Long.valueOf(sub);
            if (now.length() == 0) {
                help(res, sub, rest, target - curVal, curVal);
            } else {
                for (char op : new char[]{'+', '-', '*'}) {
                    long newTarget = target;
                    long newPreVal = preVal;
                    if (op == '+') {
                        newPreVal = curVal;
                    } else if (op == '-') {
                        newPreVal = -curVal;
                    } else if (op == '*') {
                        newTarget =  target + preVal;
                        newPreVal = preVal * curVal;
                    } 
                    help(res, now + op + sub, rest, newTarget - newPreVal, newPreVal);  
                }
            }
        }
    }
}
```
