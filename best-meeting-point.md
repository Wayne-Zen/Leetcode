[Link](https://leetcode.com/problems/best-meeting-point/)

```java
public class Solution {
    public int minTotalDistance(int[][] grid) {
        List<Integer> locX = new ArrayList<Integer>();
        List<Integer> locY = new ArrayList<Integer>();
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    locX.add(i);
                    locY.add(j);
                }
            }
        }
        int midX = locX.get(locX.size() / 2); 
        Collections.sort(locY);
        int midY = locY.get(locY.size() / 2);
        int dist = 0;
        for (int i = 0; i < locX.size(); i++) {
            dist += Math.abs(locX.get(i) - midX);
            dist += Math.abs(locY.get(i) - midY);
        }
        return dist;
    }
}
```
