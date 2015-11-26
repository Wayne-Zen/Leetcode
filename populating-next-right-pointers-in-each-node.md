[Link](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        TreeLinkNode now = root;
        TreeLinkNode head = null; // 纪录下一层的头，方便跳转到下一层
        while (now != null) {
            if (head == null && now.left != null) {
                head = now.left;
            } 
            if (now.left != null && now.right == null) {
                now = head;
                head = null;
            } else if (now.left == null && now.right == null) {
                now = head;
                head = null;
            } else if (now.left != null && now.right != null) {
                now.left.next = now.right;
                if (now.next != null) {
                    now.right.next = now.next.left;
                    now = now.next;
                } else {
                    now = head;
                    head = null;
                }
            }
        }
    }
}
```
