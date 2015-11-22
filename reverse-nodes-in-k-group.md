[Link](https://leetcode.com/problems/reverse-nodes-in-k-group/)

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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode before = dummy;
        int cnt = -1;
        while (before != null) {
            before = before.next;
            cnt++;
        }
        
        before = dummy;
        while (cnt / k > 0) {
            ListNode p1 = before.next;
            ListNode p2 = p1.next;
            ListNode save = p1;
            for (int i = 1; i < k; i++) {
                ListNode temp = p2.next;
                p2.next = p1;
                p1 = p2;
                p2 = temp;
            }
            save.next = p2;
            before.next = p1;
            cnt -= k;
            before = save;
        }
        
        return dummy.next;
    }
}
```
