[Link](https://leetcode.com/problems/palindrome-linked-list/)

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
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode fast = dummy;
        ListNode slow = dummy;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        
        ListNode p1 = slow.next;
        ListNode p2 = p1.next;
        ListNode save = p1;
        while (p2 != null) {
            ListNode temp = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = temp;
        }
        save.next = null;
        slow.next = null;
        
        while (head != null && p1 != null) {
            if (head.val != p1.val) {
                return false;
            } else {
                head = head.next;
                p1 = p1.next;
            }
        }
        return true;
    }
}
```
