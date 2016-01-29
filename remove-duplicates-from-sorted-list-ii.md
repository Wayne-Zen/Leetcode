[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode move = dummy;
        while (move.next != null) {
            if (move.next != null && move.next.next != null && move.next.val == move.next.next.val) {
                int val = move.next.val;
                while (move.next != null && move.next.val == val) {
                    move.next = move.next.next;
                }
            } else {
                move = move.next;
            }
        }
        return dummy.next;
    }
}
```
