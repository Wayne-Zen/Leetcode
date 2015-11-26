[Link](https://leetcode.com/problems/sort-list/)

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
    public ListNode sortList(ListNode head) {
        // 不能改
        if (head == null || head.next == null) {
            return head;
        }
        ListNode mid = getMid(head);
        // split
        ListNode l1 = head;
        ListNode l2 = mid.next;
        mid.next = null;
        
        return merge(sortList(l1), sortList(l2));
    }
    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode move = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                move.next = l1;
                l1 = l1.next;
                move = move.next;
            } else {
                move.next = l2;
                l2 = l2.next;
                move = move.next;
            }
        }
        while (l1 != null) {
            move.next = l1;
            l1 = l1.next;
            move = move.next;
        }
        while (l2 != null) {
            move.next = l2;
            l2 = l2.next;
            move = move.next;
        }
        return dummy.next;
    }
    private ListNode getMid(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}
```
