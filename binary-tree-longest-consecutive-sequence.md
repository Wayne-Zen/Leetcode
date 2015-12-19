[Link](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/)

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
    int max = 0;
    public int longestConsecutive(TreeNode root) {
        help(root);
        return max;
    }
    private int help(TreeNode root) {
        if (root == null) {
            return 0;
        }   
        int left = help(root.left);
        int right = help(root.right);
        int leftLen = (root.left != null && root.val == root.left.val - 1) ? left + 1 : 1;
        int rightLen = (root.right != null && root.val == root.right.val - 1) ? right + 1 : 1;
        int res = Math.max(leftLen, rightLen);
        max = Math.max(max, res);
        return res;
    }
}
```
