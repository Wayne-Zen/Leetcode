[Link](https://leetcode.com/problems/binary-tree-paths/)

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<String>();
        if (root == null) {
            return res;
        }
        help(res, String.valueOf(root.val), root);
        return res;
    }
    private void help(List<String> res, String now, TreeNode root) {
        if (root.left == null && root.right == null) {
            res.add(now);
            return;
        }
        if (root.left != null) {
            help(res, now + "->" + root.left.val, root.left);
        }
        if (root.right != null) {
            help(res, now + "->" + root.right.val, root.right);
        }
    }
}
```
