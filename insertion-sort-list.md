[Link](https://leetcode.com/problems/insertion-sort-list/)

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
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        head = head.next;
        dummy.next.next = null; //坑，切开两个链表
        while (head != null) {
            // insert head
            ListNode move = dummy;
            while (move.next != null && move.next.val < head.val) {
                move = move.next;
            }
            ListNode temp = move.next;
            move.next = head;
            head = head.next;
            move.next.next = temp;
        }
        return dummy.next;
    }
}
```
