[Link](https://leetcode.com/problems/factor-combinations/)

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (n <= 3) return result;
        helper(n, -1, result, new ArrayList<Integer>());
        return result; 
    }
    
    public void helper(int n, int lower, List<List<Integer>> result, List<Integer> cur) {
        if (lower != -1) {
            cur.add(n);
            result.add(new ArrayList<Integer>(cur));
            cur.remove(cur.size() - 1);
        }
        int upper = (int)Math.floor(Math.sqrt(n));
        for (int i = Math.max(2, lower); i <= upper; ++i) {
            if (n % i == 0) {
                cur.add(i);
                helper(n / i, i, result, cur);
                cur.remove(cur.size() - 1);
            }
        }
    }
}
```
