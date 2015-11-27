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
        // save slope as string
        int N = points.length;
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        int max = 1;
        for (int i = 0; i < N; i++) {
            Point p1 = points[i];
            int dup = 0;
            map.clear();
            map.put("origin", 1); // [[0,0],[0,0]]
            for (int j = i + 1; j < N; j++) {
                Point p2 = points[j];
                if (p1.x == p2.x && p1.y == p2.y) {
                    dup++;
                    continue;
                }
                String slope = new String();
                if (p1.x == p2.x) {
                    slope = "INF";
                } else {
                    // because (double)0/-1 is -0.0, so we should use 0.0+-0.0=0.0 to solve 0.0 !=-0.0 problem
                    slope = String.format("%.6f", 0.0 + (double)(p2.y - p1.y)/(double)(p2.x - p1.x));
                }
                if (map.containsKey(slope)) {
                    map.put(slope, map.get(slope) + 1);
                } else {
                    map.put(slope, 2);
                }
            }
            for (String s : map.keySet()) {
                max = Math.max(max, map.get(s) + dup);
            }
        }
        return max;
    }
}
```
