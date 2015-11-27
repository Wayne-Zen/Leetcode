[Link](https://leetcode.com/problems/candy/)

* 第二次遍历的时候，不能破坏第一次的结果。

```java
public class Solution {
    public int candy(int[] ratings) {
        int[] candy = new int[ratings.length];
        Arrays.fill(candy, 1);
        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i] > ratings[i - 1]) {
                candy[i] = candy[i - 1] + 1;
            }
        }
        for (int i = ratings.length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1] && candy[i] <= candy[i + 1]) {
                candy[i] = candy[i + 1] + 1;
            }
        }
        int res = 0;
        for (int i = 0; i < ratings.length; i++) {
            res += candy[i];
        }
        return res;
    }
}
```
