[Link](https://leetcode.com/problems/insert-interval/)

* 注意__置换__和拓展newInterval

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> res = new ArrayList<Interval>();
        for (Interval interval : intervals) {
            if (interval.end < newInterval.start) {
                res.add(interval);
            } else if (interval.start > newInterval.end) {
                res.add(newInterval);
                newInterval = interval;
            } else {
                int newStart = Math.min(interval.start, newInterval.start);
                int newEnd = Math.max(interval.end, newInterval.end);
                newInterval = new Interval(newStart, newEnd);
            }
        }
        res.add(newInterval);
        return res;
    }
}
```
