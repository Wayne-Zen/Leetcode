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
        if(points == null || points.length == 0) return 0;
        if(points.length == 1) return 1;
    
        // check if points have same coordinates
        for(int i=1;i<points.length;i++) {
            Point p1 = points[i-1];
            Point p2 = points[i];
            if(!isEqual(p1,p2)) {
                break;
            } else if(i == points.length - 1) {
                // here we know that no two points
                // are unequal (otherwise, we would
                // not have reached the end of the loop)
                return points.length;
            }
        }
    
        // actual points-on-line test
        int max = 0;
        for(int i=1;i<points.length;i++) {
            Point p1 = points[i-1];
            Point p2 = points[i];
    
            if(!isEqual(p1,p2)) {
                // since p1 != p2, whe know that they
                // represent a line, so we can start with 2
                int n = 2;
                for(Point p3: points) {
                    if(p3 != p1 && p3 != p2 && areOnSameLine(p1,p2,p3)) {
                        n++;
                    }
                }
                max = Math.max(max, n);
            }
        }
        return max;
    }
    
    private boolean isEqual(Point p1, Point p2) {
        return p1.x == p2.x && p1.y == p2.y;
    }
    
    private boolean areOnSameLine(Point p1, Point p2, Point p3) {
        return (p1.y - p2.y) * (p1.x - p3.x) == (p1.y - p3.y) * (p1.x - p2.x);
    }
}
```
