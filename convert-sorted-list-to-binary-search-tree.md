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
        if(head == null)
            return null;
        ListNode cur = head;
        int count = 0;
        while(cur!=null)
        {
            cur = cur.next;
            count++;
        }
        ArrayList<ListNode> list = new ArrayList<ListNode>();
        list.add(head);
        return helper(list,0,count-1);
    }
    private TreeNode helper(ArrayList<ListNode> list, int l, int r)
    {
        if(l>r)
            return null;
        int m = (l+r)/2;
        TreeNode left = helper(list,l,m-1);
        TreeNode root = new TreeNode(list.get(0).val);
        root.left = left;
        list.set(0,list.get(0).next);
        root.right = helper(list,m+1,r);
        return root;
    }
}
```
