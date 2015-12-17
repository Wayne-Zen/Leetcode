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
        
        boolean flipA = false;
        boolean flipB = false;
        ListNode saveA = headA;
        ListNode saveB = headB;
        while (headA != null && headB != null && headA != headB) {
            if (headA.next == null && !flipA) {
                headA = saveB;
                flipA = !flipA;
            } else {
                headA = headA.next;
            }
            if (headB.next == null && !flipB) {
                headB = saveA;
                flipB = !flipB;
            } else {
                headB = headB.next;
            }
        }
        if (headA == null || headB == null) {
            return null;
        } else {
            return headA;
        }
    }
}
```
