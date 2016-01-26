[Link](https://leetcode.com/problems/missing-ranges/)

```java
public class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> res = new ArrayList<String>();
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == upper) {
                upper--;
                break;
            } else if (nums[i] > upper) {
                break;
            }
            
            if (nums[i] == lower) {
                lower++;
            } else if (nums[i] == lower + 1) {
                res.add(lower + "");
                lower = nums[i] + 1;
            } else if (nums[i] > lower + 1) {
                res.add(lower + "->" + (nums[i] - 1));
                lower = nums[i] + 1;
            }
        }
        if (upper == lower) {
            res.add(lower + "");
        } else if (lower < upper){
            res.add(lower + "->" + upper);
        } 
        return res;
    }
}
```
