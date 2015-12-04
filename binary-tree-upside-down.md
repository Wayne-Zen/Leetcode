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
        TreeNode prev = null, right = null, next = null;
        while(root != null){
            next = root.left;
            root.left = right;
            right = root.right;
            root.right = prev;
            prev = root;
            root = next;
        }
        return prev;
    }
}
```
