[Link](https://leetcode.com/problems/max-points-on-a-line/)

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
public class Solution {
    public int maxPoints(Point[] points) {
        if (points == null || points.length == 0) {
            return 0;
        }
        int max = 0;
        for (int i = 0; i < points.length; i++) {
            // slope -> count
            HashMap<String, Integer> map = new HashMap<String, Integer>();
            map.put("origin", 1);
            int dup = 0;
            for (int j = i + 1; j < points.length; j++) {
                Point p1 = points[i];
                Point p2 = points[j];
                if (p1.x == p2.x && p1.y == p2.y) {
                    dup++;
                    continue;
                }
                String slope = "";
                if (p1.x == p2.x) {
                    slope = "INF";
                } else {
                    slope = String.format("%.6f", 0.0 + (double)(p1.y - p2.y) / (p1.x - p2.x));
                }
                map.put(slope, map.containsKey(slope) ? map.get(slope) + 1 : 2);
            }
            for (int cnt : map.values()) {
                max = Math.max(max, cnt + dup);
            }
        }
        return max;
    }
}
```
