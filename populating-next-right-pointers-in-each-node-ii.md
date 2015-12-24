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

        TreeLinkNode nextLevelHead = root;
        
        while (nextLevelHead != null) {
            TreeLinkNode move = nextLevelHead;
            nextLevelHead = null;
            TreeLinkNode prev = null;
            while (move != null) {
                if (move.left != null && move.right != null) {
                    if (nextLevelHead == null) {
                        nextLevelHead = move.left;
                    }
                    if (prev != null) {
                        prev.next = move.left;
                    }
                    move.left.next = move.right;
                    prev = move.right;
                } else if (move.left != null && move.right == null) {
                    if (nextLevelHead == null) {
                        nextLevelHead = move.left;
                    }
                    if (prev != null) {
                        prev.next = move.left;
                    }
                    prev = move.left;
                } else if (move.left == null && move.right != null) {
                    if (nextLevelHead == null) {
                        nextLevelHead = move.right;
                    }
                    if (prev != null) {
                        prev.next = move.right;
                    }
                    prev = move.right;
                }
                move = move.next;
            }    
        }
    }
}
```
