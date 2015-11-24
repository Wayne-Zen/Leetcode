[Link](https://leetcode.com/problems/rotate-list/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || k == 0) {
            return head;
        }
        
        ListNode fast = head;
        ListNode slow = head;
        int cnt = 1;
        ListNode move = head;
        while (move.next != null) {
            move = move.next;
            cnt++;
        }
        for (int i = 0; i < k % cnt; i++) {
            if (fast.next != null) {
                fast = fast.next;
            } else {
                fast = head;
            }
        }
        if (fast == slow) {
            return head;
        }
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        ListNode res = slow.next;
        fast.next = head;
        slow.next = null;
        return res;
        
    }
}
```
