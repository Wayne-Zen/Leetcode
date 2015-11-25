[Link](https://leetcode.com/problems/balanced-binary-tree/)

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
    public boolean isBalanced(TreeNode root) {
        return check(root) != -1;
    }
    
    private int check(TreeNode root) {
        // negative -> not balance
        // non-negative -> depth
        if (root == null) {
            return 0;
        }
        int left = check(root.left);
        int right = check(root.right);
        if (left == -1 || right == -1) {
            return -1;
        }
        if (Math.abs(left - right) > 1) {
            return -1;
        }
        return 1 + Math.max(left, right);
    }
}
```
