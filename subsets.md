[Link](https://leetcode.com/problems/subsets/)

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, nums, 0);
        return res;
    }
    private void help(List<List<Integer>> res,
                      List<Integer> now, 
                      int[] nums, int pos) {
        res.add(new ArrayList<Integer>(now));
        
        for (int i = pos; i < nums.length; i++) {
            now.add(nums[i]);
            help(res, now, nums, i + 1);
            now.remove(now.size() -1 );
        }
    }
}
```
