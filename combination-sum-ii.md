[Link](https://leetcode.com/problems/combination-sum-ii/)


```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, candidates, target, 0);
        return res;
    }
    
    private void help(List<List<Integer>> res,
                      List<Integer> now,
                      int[] candidates,
                      int target, int pos) {
        if (target == 0) {
            res.add(new ArrayList<Integer>(now));
            return;
        }
        for (int i = pos; i < candidates.length; i++) {
            if (i > pos && candidates[i] == candidates[i - 1]) {
                continue;
            }
            if (candidates[i] > target) {
                break;
            }
            now.add(candidates[i]);
            target -= candidates[i];
            help(res, now, candidates, target, i + 1); //  i + 1 to select once
            now.remove(now.size() - 1);
            target += candidates[i];
        }
    }
}
```
