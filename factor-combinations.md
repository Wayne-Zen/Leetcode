[Link](https://leetcode.com/problems/factor-combinations/)

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (n == 1) {
            return res;
        }
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, n, 2, 1);
        return res;
    }
    private void help(List<List<Integer>> res, 
                      List<Integer> now, int n, 
                      int start, int product) {
        if (n == product) {
            res.add(new ArrayList<Integer>(now));
            return;
        }
        for (int i = start; i < n; i++) {
            if (i * product > n) {
                break;
            }
            if (n % i != 0) {
                continue;
            }
            now.add(i);
            help(res, now, n, i, i * product);
            now.remove(now.size() - 1);
        }
    }
}
```
