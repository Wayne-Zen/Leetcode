[Link](https://leetcode.com/problems/combination-sum/)

* help(res, now, candidates, target, i);// use i

```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        Arrays.sort(candidates);
        help(res, now, candidates, target, 0);
        return res;
    }
    private void help(List<List<Integer>> res, List<Integer> now,
                      int[] candidates, int target, int pos) {
        if (target == 0) {
            res.add(new ArrayList<Integer>(now));
            return;
        }
        for (int i = pos; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }
            now.add(candidates[i]);
            help(res, now, candidates, target - candidates[i], i);
            now.remove(now.size() - 1);
        }
    }
}
```
