[Link](https://leetcode.com/problems/pascals-triangle-ii/)

```java
public class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> row = new ArrayList<Integer>();
        row.add(1);
        for (int i = 1; i <= rowIndex; i++) {
            List<Integer> newRow = new ArrayList<Integer>();
            for (int j = 0; j <= row.size(); j++) {
                if (j == 0 || j == row.size()) {
                    newRow.add(1);
                } else {
                    newRow.add(row.get(j - 1) + row.get(j));
                }
            }
            row = newRow;
        }
        return row;
    }
}
```
