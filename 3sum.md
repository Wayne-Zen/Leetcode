[Link](https://leetcode.com/problems/3sum/)

```java
public class Solution {
    /**
     * @param numbers : Give an array numbers of n integer
     * @return : Find all unique triplets in the array which gives the sum of zero.
     */
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (nums == null || nums.length < 3) {
            return res;
        }
        Arrays.sort(nums);
        
        // 不可提前去重; e.g [-1, -1, 2]
        for (int i = 0; i < nums.length; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
				continue; // to skip duplicate numbers; e.g [0,0,0,0]
			}
			
			int target = -nums[i];
			if (target < 0) {
			    break;
			}
            int head = i + 1;
            int tail = nums.length - 1;
            while (head < tail) {
                
                int sum = nums[head] + nums[tail];
                if (sum < target) {
                    head++;
                } else if (sum > target) {
                    tail--;
                } else {
                    List<Integer> tmp = new ArrayList<Integer>();
					tmp.add(nums[i]);
					tmp.add(nums[head]);
					tmp.add(nums[tail]);
					res.add(tmp);
					// do forget
					head++;
					tail--;
					// to skip duplicates
					while (head < tail && nums[head] == nums[head - 1]) { 
						head++;
					}
					while (head < tail && nums[tail] == nums[tail + 1]) { 
						tail--;
					}
                }
            }
        }
        return res;
    }
}
```
