[Link](https://leetcode.com/problems/different-ways-to-add-parentheses/)

```java
import java.util.regex.*;

public class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        Pattern pattern = Pattern.compile("((\\d*\\.\\d+)|(\\d+)|([\\+\\-\\*/\\(\\)]))");
        Matcher m = pattern.matcher(input);
        List<String> all = new ArrayList<String>();
        while(m.find()) {
            all.add(m.group());
        }
        return help(all, 0, all.size() - 1);
    }
    
    private List<Integer> help(List<String> s, int lo, int hi) {
        List<Integer> res = new ArrayList<Integer>();
        if (lo == hi) {
            res.add(Integer.valueOf(s.get(lo)));
            return res;
        }
        
        for (int i = lo + 1; i < hi; i+=2) {
            List<Integer> l1 = help(s, lo, i - 1);
            List<Integer> l2 = help(s, i + 1, hi);
            for (int v1 : l1) {
                for (int v2 : l2) {
                    String op = s.get(i);
                    if (op.equals("+")) {
                        res.add(v1 + v2);
                    } else if (op.equals("-")) {
                        res.add(v1 - v2);
                    } else if (op.equals("*")) {
                        res.add(v1 * v2);
                    } else if (op.equals("/")) {
                        res.add(v1 / v2);
                    }
                }
            }
        }
        return res;
    }
}
```
