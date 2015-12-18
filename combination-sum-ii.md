[Link](https://leetcode.com/problems/combination-sum-ii/)


```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
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
            if (i > pos && candidates[i - 1] == candidates[i]) {
                continue;
            }
            now.add(candidates[i]);
            help(res, now, candidates, target - candidates[i], i + 1);
            now.remove(now.size() - 1);
        }
    }
}
```
