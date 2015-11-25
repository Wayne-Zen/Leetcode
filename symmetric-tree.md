[Link](https://leetcode.com/problems/symmetric-tree/)

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isSym(root.left, root.right);
    }
    private boolean isSym(TreeNode left, TreeNode right) {
        if (left == null) {
            return right == null;
        }
        if (right == null) {
            return left == null;
        }
        if (left.val != right.val) {
            return false;
        }
        return isSym(left.right, right.left) && isSym(left.left, right.right);
    }
}
```
