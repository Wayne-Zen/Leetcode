[Link](https://leetcode.com/problems/permutations-ii/)

* 相等的时候则前面的数必须使用了，自己才能使用

```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        boolean[] visited = new boolean[nums.length];
        help(res, now, visited, nums);
        return res;
    }
    
    private void help(List<List<Integer>> res,
                      List<Integer> now,
                      boolean[] visited, int[] nums) {
        if (now.size() == nums.length) {
            res.add(new ArrayList<Integer>(now));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (visited[i] || (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1])) {
                continue;
            }
            now.add(nums[i]);
            visited[i] = true;
            help(res, now, visited, nums);
            visited[i] = false;
            now.remove(now.size() - 1);
        }
    }
}
```
