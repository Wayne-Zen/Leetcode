[Link](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

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
    public int maxPathSum(TreeNode root) {
        // res[0]: single path, can contains zero node
        // res[1]: global path, must contains at least one node
        int[] res = help(root);
        return res[1];
    }
    private int[] help(TreeNode root) {
        if (root == null) {
            return new int[]{0, Integer.MIN_VALUE};
        }
        int[] left = help(root.left);
        int[] right = help(root.right);
        int singlePath = Math.max(0, Math.max(left[0], right[0]) + root.val);
        int globalPath = Math.max(root.val + left[0] + right[0], Math.max(left[1], right[1]));
        return new int[]{singlePath, globalPath};
    }
}
```
