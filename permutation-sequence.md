[Link](https://leetcode.com/problems/permutation-sequence/)

* k = k - 1; kth -> index

```java
public class Solution {
    public String getPermutation(int n, int k) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int i = 1; i <= n; i++) {
            list.add(i);
        }
        int[] fact = new int[n];
        fact[0] = 1;
        for (int i = 1; i < n; i++) {
            fact[i] = fact[i - 1] * i;
        }
        StringBuilder sb = new StringBuilder();
        k = k - 1;
        while (list.size() != 0) {
            int digit = list.get(k / fact[n - 1]);
            sb.append(digit);
            list.remove(Integer.valueOf(digit));
            k = k % fact[n - 1];
            n--;
        }
        return sb.toString();
    }
}
```
