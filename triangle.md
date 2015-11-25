[Link](https://leetcode.com/problems/triangle/)

```java
public class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        ArrayList<Integer> sum = new ArrayList<Integer>();
        sum.add(triangle.get(0).get(0));
        for (int i = 1; i < triangle.size(); i++) {
            ArrayList<Integer> newSum = new ArrayList<Integer>();
            for (int j = 0; j < triangle.get(i).size(); j++) {
                int val = triangle.get(i).get(j);
                if (j == 0) {
                    newSum.add(val + sum.get(j));
                } else if (j == triangle.get(i).size() - 1) {
                    newSum.add(val + sum.get(j - 1)); 
                } else {
                    newSum.add(val + Math.min(sum.get(j - 1), sum.get(j)));
                }
            }
            sum = newSum;
        }
        return Collections.min(sum);
    }
}
```
