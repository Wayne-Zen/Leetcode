[link](https://leetcode.com/problems/combinations/)

* help的pos要穿入i＋1

```java
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, n, k, 1);
        return res;
    }
    private void help(List<List<Integer>> res,
                      List<Integer> now,
                      int n, int k, int pos) {
        if (k == 0) {
            res.add(new ArrayList<Integer>(now));
            return;
        };
        for (int i = pos; i <= n; i++) {
            now.add(i);
            help(res, now, n, k - 1, i + 1);
            now.remove(now.size() - 1);
        }
    }
}
```
