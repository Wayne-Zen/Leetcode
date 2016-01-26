[Link](https://leetcode.com/problems/factor-combinations/)

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (n <= 3) return res;
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, n, 2, n);
        return res;
    }
    private void help(List<List<Integer>> res, List<Integer> now, int n, int base, int init) {
        if (n == 1) {
            if (now.size() == 1 && now.get(0) == init) {
                return;
            }
            res.add(new ArrayList<Integer>(now));
            return;
        }
        for (int i = base; i <= n; i++) {
            if (n % i != 0) {
                continue;
            }
            now.add(i);
            help(res, now, n / i, i, init);
            now.remove(now.size() - 1);
        }
    }
}
```
