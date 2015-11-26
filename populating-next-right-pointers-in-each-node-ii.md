[Link](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

* 可以直接应用于 populating-next-right-pointers-in-each-node

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
        if (root == null) {
            return;
        }   
        TreeLinkNode last = null; // 构建层的上一个节点
        TreeLinkNode head = null; // 构建层的头节点
        TreeLinkNode now = root;
        while (now != null) {
            if (head == null && (now.left != null || now.right != null)) {
                if (now.left != null) {
                    head = now.left;
                } else {
                    head = now.right;
                }
            }
            
            if (now.left != null && now.right != null) {
                if (last != null) {
                    last.next = now.left;
                }
                now.left.next = now.right;
                last = now.right;
            } else if (now.left != null && now.right == null) {
                if (last != null) {
                    last.next = now.left;
                }
                last = now.left;
            } else if (now.left == null && now.right != null) {
                if (last != null) {
                    last.next = now.right;
                }
                last = now.right;   
            }
                
            
            if (now.next == null) {
                now = head;
                head = null;
                last = null;
            } else {
                now = now.next;
            }
        }
    }
}
```
