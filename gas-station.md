[Link](https://leetcode.com/problems/gas-station/)

```java
public class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        // 如果不能跑完，最后total<0
        int index = 0;
        int sum = 0;
        int total = 0;
        for (int i = 0; i < cost.length; i++) {
            sum += gas[i] - cost[i];
            total += gas[i] - cost[i];
            if (sum < 0) {
                sum = 0;
                index = i + 1;
            } 
        }
        if (total < 0) {
            return -1;
        }
        return index;
    }
}
```
