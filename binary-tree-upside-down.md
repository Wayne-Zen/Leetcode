[Link](https://leetcode.com/problems/binary-tree-upside-down/)

```java
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
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        TreeNode parent = null;
        TreeNode parentRight = null;
        while (root != null) {
            TreeNode next = root.left;
            root.left = parentRight;
            parentRight = root.right;
            root.right = parent;
            parent = root;
            root = next;
        }
        return parent;
    }
}
```
