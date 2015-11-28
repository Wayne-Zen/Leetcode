[Link](https://leetcode.com/problems/count-complete-tree-nodes/)

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
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int lc = 1;
        int rc = 1;
        TreeNode l = root.left;
        while (l != null) {
            lc++;
            l = l.left;
        }
        TreeNode r = root.right;
        while (r != null) {
            rc++;
            r = r.right;
        }
        if (lc == rc) {
            return (1 << lc) - 1;
        } else {
            return 1 + countNodes(root.left) + countNodes(root.right);
        }
    }
}
```
