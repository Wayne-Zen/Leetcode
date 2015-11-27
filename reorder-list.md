[Link](https://leetcode.com/problems/reorder-list/)


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
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }
        
        // 切分
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode fast = dummy;
        ListNode slow = dummy;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        
        // 翻转
        ListNode p1 = slow.next;
        ListNode p2 = p1.next;
        ListNode save = p1;
        while (p2 != null) {
            ListNode tmp = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = tmp;
        }
        save.next = p2;
        slow.next = null;
        
        // 合并
        ListNode move = dummy;
        while (head != null && p1 != null) {
            move.next = head;
            head = head.next;
            move = move.next;
            
            move.next = p1;
            p1 = p1.next;
            move = move.next;
        }
        move.next = head; //slow是n/2，但是从n/2＋1开始翻转，head链比较长
        head = dummy.next;
    }
}
```
