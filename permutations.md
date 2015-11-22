[Link](https://leetcode.com/problems/permutations/)

```java
public class Solution {
    public List<List<Integer>> permute(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        boolean[] visited = new boolean[nums.length];
        help(res, now, nums, visited);
        return res;
    }
    
    private void help(List<List<Integer>> res,
                      List<Integer> now,
                      int[] nums, boolean[] visited) {
        if (now.size() == nums.length) {
            res.add(new ArrayList<Integer>(now));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            now.add(nums[i]);
            visited[i] = true;
            help(res, now, nums, visited);
            now.remove(now.size() - 1);
            visited[i] = false;
        }
    }
}
```
