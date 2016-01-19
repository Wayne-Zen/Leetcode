[Link](https://leetcode.com/problems/odd-even-linked-list/)

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
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenSave = even;
        ListNode move = head.next.next;
        while (move != null && move.next != null) {
            odd.next = move;
            even.next = move.next;
            
            odd = odd.next;
            even = even.next;
            move = move.next.next;
        }
        if (move != null) {
            odd.next = move;
            odd = odd.next;
        }
        odd.next = evenSave;
        even.next = null;
        return head;
    }
}
```
