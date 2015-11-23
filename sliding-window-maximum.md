[Link](https://leetcode.com/problems/sliding-window-maximum/)

* 双端队列，递减，头即为最大值
* deque 纪录的是index

```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k == 0) {
            return new int[0];
        }
        
        LinkedList<Integer> deque = new LinkedList<Integer>();
        int[] res = new int[nums.length - k + 1];
        
        for (int i = 0; i < nums.length; i++) {
            // head
            if (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }
            
            // tail
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }
            deque.offerLast(i);
            
            // result
            if (i >= k - 1) {
                res[i - k + 1] = nums[deque.peekFirst()];    
            }
        }
        
        return res;
    }
}
```
