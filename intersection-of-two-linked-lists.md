[Link](https://leetcode.com/problems/intersection-of-two-linked-lists/)

```java
/**
 * Definition for singly-linked list.
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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode cpA = headA;
        boolean flipA = false;
        ListNode cpB = headB;
        boolean flipB = false;
        while (headA != null && headB != null && headA != headB) {
            if (!flipA && headA.next == null) {
                headA = cpB;
                flipA = true;
            } else {
                headA = headA.next;
            }
            if (!flipB && headB.next == null) {
                headB = cpA;
                flipB = true;
            } else {
                headB = headB.next;
            }
        }
        if (headA == null || headB == null) {
            return null;
        }
        return headA;
    }
}
```
