[Link](https://leetcode.com/problems/4sum/)


```java
public class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 3; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j != i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int head = j + 1;
                int tail = nums.length - 1;
                int goal = target - nums[i] - nums[j];
                while (head < tail) {
                    if (nums[head] + nums[tail] < goal) {
                        head++;
                    } else if (nums[head] + nums[tail] > goal) {
                        tail--;
                    } else {
                        List<Integer> sub = new ArrayList<Integer>();
                        sub.add(nums[i]);
                        sub.add(nums[j]);
                        sub.add(nums[head]);
                        sub.add(nums[tail]);
                        res.add(sub);
                        head++;
                        tail--;
                        while (head < tail && nums[head] == nums[head - 1]) {
                            head++;
                        }
                        while (head < tail && nums[tail] == nums[tail + 1]) {
                            tail--;
                        }
                    }
                }
            }
        }
        return res;
    }
}
```
