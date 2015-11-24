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
    private class MyComparator implements Comparator<Interval> {
        @Override
        public int compare(Interval in1, Interval in2) {
            return in1.start - in2.start;
        }
    }
    
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() == 0 || intervals.size() == 1) {
            return intervals;
        }
        // sort
        Collections.sort(intervals, new MyComparator());
        List<Interval> res = new ArrayList<Interval>();
        Interval newIn = intervals.get(0);
        for (int i = 1; i < intervals.size(); i++) {
            Interval in = intervals.get(i);
            if (newIn.end < in.start) {
                res.add(new Interval(newIn.start, newIn.end));
                newIn = in;
                continue;
            }
            if (newIn.end >= in.start) {
                int newEnd = Math.max(newIn.end, in.end);
                newIn = new Interval(newIn.start, newEnd);
            }
        }
        res.add(newIn);
        return res;
    }
}
```
