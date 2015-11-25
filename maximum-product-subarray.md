[Link](https://leetcode.com/problems/maximum-product-subarray/)

* 记录min/max product两个状态
* 更新最大最小值，有交叉使用的部分，先批量计算，后批量更新

```java
public class Solution {
    public int maxProduct(int[] nums) {
        int lastMax = nums[0]; // max including last number
        int lastMin = nums[0];
        int max = nums[0]; // history
        for (int i = 1; i < nums.length; i++) {
            int newMax = Math.max(Math.max(lastMax * nums[i], lastMin * nums[i]), nums[i]);
            int newMin = Math.min(Math.min(lastMax * nums[i], lastMin * nums[i]), nums[i]);
            max = Math.max(max, newMax);
            lastMax = newMax;
            lastMin = newMin;
        }
        return max;
    }
}
```
