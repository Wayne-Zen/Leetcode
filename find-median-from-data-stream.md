[Link](https://leetcode.com/problems/find-median-from-data-stream/)

```java
class MedianFinder {
    int size = 0;
    PriorityQueue<Integer> q1 = new PriorityQueue<Integer>(11, Collections.reverseOrder()); // max, size/2 (+1)
    PriorityQueue<Integer> q2 = new PriorityQueue<Integer>(); // min, size/2
    
    // Adds a number into the data structure.
    public void addNum(int num) {
        size++;
        q1.offer(num);
        if (q1.size() - q2.size() == 2) {
            q2.offer(q1.poll());
        }
        // 保证q1全部小于q2
        if (!q2.isEmpty() && q1.peek() > q2.peek()) {
            int n1 = q1.poll();
            int n2 = q2.poll();
            q1.offer(n2);
            q2.offer(n1);
        }
    }

    // Returns the median of current data stream
    public double findMedian() {
        if (size % 2 == 0) {
            return (q1.peek() + q2.peek()) / (double)2;
        } else {
            return (double)(q1.peek());
        }
    }
};

// Your MedianFinder object will be instantiated and called as such:
// MedianFinder mf = new MedianFinder();
// mf.addNum(1);
// mf.findMedian();
```
