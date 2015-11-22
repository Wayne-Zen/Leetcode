[Link](https://leetcode.com/problems/merge-two-sorted-lists/)

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode now = dummy;
        while (l1 != null && l2 != null) {
            int v1 = l1.val;
            int v2 = l2.val;
            if (v1 < v2) {
                now.next = l1;
                now = now.next;
                l1 = l1.next;
            } else {
                now.next = l2;
                now = now.next;
                l2 = l2.next;
            }
        }
        while (l1 != null) {
            now.next = l1;
            now = now.next;
            l1 = l1.next;
        } 
        while (l2 != null) {
            now.next = l2;
            now = now.next;
            l2 = l2.next;
        }
        return dummy.next;
    }
}
```
