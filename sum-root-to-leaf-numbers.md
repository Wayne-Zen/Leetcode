[Link](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

* 累加结果使用全局变量或长度为1的数组

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
    int res = 0;
    public int sumNumbers(TreeNode root) {
        if (root == null) {
            return 0;
        }
        help(root, 0);
        return res;
    }
    private void help(TreeNode root, int val) {
        if (root.left == null && root.right == null) {
            res += val * 10 + root.val;
        }
        if (root.left != null) {
            help(root.left, val * 10 + root.val);
        }
        if (root.right != null) {
            help(root.right, val * 10 + root.val);
        }
    }
}
```
