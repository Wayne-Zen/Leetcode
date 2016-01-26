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
        ListNode oddDummy = new ListNode(-1);
        ListNode evenDummy = new ListNode(-1);
        ListNode oddMove = oddDummy;
        ListNode evenMove = evenDummy;
        int index = 1;
        while (head != null) {
            if (index % 2 == 1) {
                oddMove.next = head;
                head = head.next;
                oddMove = oddMove.next;
            } else {
                evenMove.next = head;
                head = head.next;
                evenMove = evenMove.next;
            }
            index++;
        }
        oddMove.next = evenDummy.next;
        evenMove.next = null;
        return oddDummy.next;
    }
}
```
