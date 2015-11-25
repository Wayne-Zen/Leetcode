[Link](https://leetcode.com/problems/pascals-triangle/)

```java
public class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (numRows == 0) {
            return res;
        }
        List<Integer> row = new ArrayList<Integer>();
        row.add(1);
        res.add(row);
        for (int i = 1; i < numRows; i++) {
            List<Integer> newRow = new ArrayList<Integer>();
            for (int j = 0; j <= row.size(); j++) {
                if (j == 0) {
                    newRow.add(1);
                } else if (j == row.size()) {
                    newRow.add(1);
                } else {
                    newRow.add(row.get(j - 1) + row.get(j));
                }
            }
            res.add(newRow);
            row = newRow;
        }
        
        return res;
    }
}
```
