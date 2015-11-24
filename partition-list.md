[Link](https://leetcode.com/problems/partition-list/)

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
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return head;
        }
        ListNode d1 = new ListNode(-1);
        ListNode d2 = new ListNode(-1);
        ListNode m1 = d1;
        ListNode m2 = d2;
        while (head != null) {
            if (head.val < x) {
                m1.next = head;
                m1 = m1.next;
            } else {
                m2.next = head;
                m2 = m2.next;
            }
            head = head.next;
        }
        m2.next = null;
        m1.next = d2.next;
        return d1.next;
    }
}
```
