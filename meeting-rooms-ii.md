[Link](https://leetcode.com/problems/meeting-rooms-ii/)

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
    class MyComparator implements Comparator<Interval>{
        public int compare(Interval in1, Interval in2) {
            return in1.start - in2.start;
        }
    }
    public int minMeetingRooms(Interval[] intervals) {
        if (intervals == null || intervals.length == 0) {
            return 0;
        }
        Arrays.sort(intervals, new MyComparator());
        int cnt = 1;
        PriorityQueue<Integer> heap = new PriorityQueue<Integer>();
        heap.offer(intervals[0].end);
        for (int i = 1; i < intervals.length; i++) {
            Interval in = intervals[i];
            if (in.start < heap.peek()) {
                cnt++;
                heap.offer(in.end);
            } else {
                heap.poll();
                heap.offer(in.end);
            }
        }
        return cnt;
    }
}
```
