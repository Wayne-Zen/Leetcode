[Link](https://leetcode.com/problems/merge-intervals/)

* 先排序，排序之后还可以消除一半的分支
* 把前一个interval 看做insert interval

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
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() == 0 || intervals.size() == 1) {
            return intervals;
        }
        // sort
        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval in1, Interval in2) {
                return in1.start - in2.start;
            }
        });
        List<Interval> res = new ArrayList<Interval>();
        Interval newInterval = intervals.get(0);
        for (int i = 1; i < intervals.size(); i++) {
            Interval interval= intervals.get(i);
            if (newInterval.end < interval.start) {
                res.add(newInterval);
                newInterval = interval;
            } else if (newInterval.end >= interval.start) {
                int newEnd = Math.max(newInterval.end, interval.end);
                newInterval = new Interval(newInterval.start, newEnd);
            }
        }
        res.add(newInterval);
        return res;
    }
}
```
