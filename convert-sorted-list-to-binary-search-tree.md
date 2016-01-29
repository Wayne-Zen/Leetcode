[Link](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

* 注意fast停止条件, fast != tail && fast.next != tail

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        return build(head, null);
    }
    
    private TreeNode build(ListNode head, ListNode tail) {
        if(head == tail) {
            return null;
        }
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;
        while (fast != tail && fast.next != tail) {
            fast = fast.next.next;
            slow = slow.next;
        }
        TreeNode root = new TreeNode(slow.val);
        root.left = build(head, slow);
        root.right = build(slow.next, tail);
        return root;
    }
}
```


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) {
            return null;
        }
        int size = 0;
        ListNode move = head;
        while (move != null) {
            size++;
            move = move.next;
        }
        return help(new ListNode[]{head}, size);
    }
    private TreeNode help(ListNode[] head, int size) {
        if (size <= 0) {
            return null;
        }
        TreeNode left = help(head, size / 2);
        TreeNode root = new TreeNode(head[0].val);
        head[0] = head[0].next;
        TreeNode right = help(head, size - size / 2 - 1);
        
        root.left = left;
        root.right = right;
        return root;
    }
}
```
