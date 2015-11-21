[Link](https://leetcode.com/problems/add-two-numbers/)

* update now, l1, l2 to next
* init: now = dummy
* 最后判断carry是否为1


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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int carry = 0;
        ListNode dummy = new ListNode(-1);
        ListNode now = dummy;
        while (l1 != null && l2 != null) {
            int sum = l1.val + l2.val + carry;
            carry = sum / 10;
            sum = sum % 10;
            now.next = new ListNode(sum);
            now = now.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        while (l1 != null) {
            int sum = l1.val + carry;
            carry = sum / 10;
            sum = sum % 10;
            now.next = new ListNode(sum);
            now = now.next;
            l1 = l1.next;
        }
        while (l2 != null) {
            int sum = l2.val + carry;
            carry = sum / 10;
            sum = sum % 10;
            now.next = new ListNode(sum);
            now = now.next;
            l2 = l2.next;
        }
        if (carry == 1) {
            now.next = new ListNode(1);
        }
        
        return dummy.next;
    }
}
```
