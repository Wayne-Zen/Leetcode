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
        for (int i = 0; i < intervals.size(); i++) {
            Interval in = intervals.get(i);
            if (in.end < newInterval.start) {
                res.add(new Interval(in.start, in.end));
                continue;
            } 
            if (newInterval.end < in.start) {
                res.add(new Interval(newInterval.start, newInterval.end));
                newInterval = in;
                continue;
            }
            if (in.end >= newInterval.start || in.start <= newInterval.end) {
                int newStart = Math.min(in.start, newInterval.start);
                int newEnd = Math.max(in.end, newInterval.end);
                newInterval = new Interval(newStart, newEnd);
            }
        }
        res.add(newInterval);
        return res;
    }
}
```
