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
        
        while (head != null) {
            ListNode move = dummy;
            while (move.next != null && head.val > move.next.val) {
                move = move.next;
            }
            ListNode temp = head.next;
            head.next = move.next;
            move.next = head;
            move = move.next.next;
            head = temp;
        }
        return dummy.next;
    }
}
```
