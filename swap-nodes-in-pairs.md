[Link](https://leetcode.com/problems/swap-nodes-in-pairs/)

<img src="img/Photos/swap-nodes-in-pairs.png" width="400">

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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode n1, n2, n3, n4;
        n1 = dummy;
        while (true) {
            if (n1 == null) {
                break;
            }
            n2 = n1.next;
            if (n2 == null) {
                break;
            }
            n3 = n1.next.next;
            if (n3 == null) {
                break;
            }
            n4 = n1.next.next.next;
            n1.next = n3;
            n3.next = n2;
            n2.next = n4;
            // 坑： 已经交换过了
            n1 = n2;
        }
        return dummy.next;
    }
}
```
