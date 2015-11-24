[Link](https://leetcode.com/problems/permutation-sequence/)

* k = k - 1; kth -> index

```java
public class Solution {
    public String getPermutation(int n, int k) {
        int[] factor = new int[n];
        factor[0] = 1;
        ArrayList<Integer> nums = new ArrayList<Integer>();
        nums.add(1);
        for (int i = 1; i < n; i++) {
            factor[i] = factor[i - 1] * i;
            nums.add(i + 1);
        }
        k = k - 1;
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            int index = k / factor[n - 1 - i];
            sb.append(nums.get(index));
            nums.remove(index);
            k = k % factor[n - 1 - i];
        }
        return sb.toString();
    }
}
```
