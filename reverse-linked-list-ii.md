[Link](https://leetcode.com/problems/reverse-linked-list-ii/)


```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (m >= n || head == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode before = dummy;
        
        for (int i = 0; i < m - 1; i++) {
            before = before.next;
        }
        
        ListNode p1 = before.next;
        ListNode p2 = p1.next;
        ListNode save = p1;
        for (int i = m; i < n; i++) {
            ListNode temp = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = temp;
        }
        save.next = p2;
        before.next = p1;
        
        return dummy.next;
    }
}
```
