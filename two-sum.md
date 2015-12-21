[Link](https://leetcode.com/problems/two-sum/)

* 定义comparator，排序index
* index 数组一定要是 Integer[]
* head, tail 是index的index，获取下标使用index[head], 获取值使用nums[index[head]]

```java
import java.util.*;

public class Solution {
    private class MyComparator implements Comparator<Integer> {
        private final int[] nums;
        public MyComparator(int[] nums) {
            this.nums = nums;
        }
        @Override
        public int compare(Integer i1, Integer i2) {
            return nums[i1] - nums[i2];
        }
    }
    
    public int[] twoSum(int[] nums, int target) {
        Integer[] index = new Integer[nums.length];
        for (int i = 0; i < nums.length; i++) {
            index[i] = i;
        }
        Arrays.sort(index, new MyComparator(nums));
        int head = 0;
        int tail = nums.length - 1;
        while (nums[index[head]] + nums[index[tail]] != target) {
            if (nums[index[head]] + nums[index[tail]] < target) {
                head++;
            } else {
                tail--;
            }
        }
        int[] ans = new int[2];
        ans[0] = Math.min(index[head], index[tail]) + 1;
        ans[1] = Math.max(index[head], index[tail]) + 1;
        return ans;
    }
}
```

```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
		HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
		int n = numbers.length;
		int[] result = new int[2];
		for (int i = 0; i < numbers.length; i++) {
            if (map.containsKey(target - numbers[i])) {
                result[0] = map.get(target-numbers[i]) + 1;
                result[1] = i + 1;
                break;
            }
            else {
                map.put(numbers[i], i);
            }
        }
		return result;
    }
}
```
