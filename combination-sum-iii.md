[Link](https://leetcode.com/problems/combination-sum-iii/)

```java
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, k, n, 1);
        return res;
    }
    
    private void help(List<List<Integer>> res,
                      List<Integer> now,
                      int k, int n, int start) {
        if (k == 0) {
            if (n == 0) {
                res.add(new ArrayList<Integer>(now));
            }
            return;
        }

        for (int i = start; i < 10; i++) {
            if (i > n) {
                break;
            }
            now.add(i);
            help(res, now, k - 1, n - i, i + 1);
            now.remove(now.size() - 1);
        }
    }
}
```
