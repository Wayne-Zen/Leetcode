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
        TreeNode lmove = root;
        int lc = 0;
        while (lmove != null) {
            lc++;
            lmove = lmove.left;
        }
        TreeNode rmove = root;
        int rc = 0;
        while (rmove != null) {
            rc++;
            rmove = rmove.right;
        }
        if (lc == rc) {
            return (1 << lc) - 1;
        } else {
            return 1 + countNodes(root.left) + countNodes(root.right);
        }
    }
}
```

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
        return help(root, -1, -1);
    }
    private int help(TreeNode root, int lcnt, int rcnt) {
        TreeNode lmove = root;
        int lc = 0;
        if (lcnt == -1) {
            while (lmove != null) {
                lc++;
                lmove = lmove.left;
            }
        } else {
            lc = lcnt;
        }
        TreeNode rmove = root;
        int rc = 0;
        if (rcnt == -1) {
            while (rmove != null) {
                rc++;
                rmove = rmove.right;
            }
        } else {
            rc = rcnt;
        }
        if (lc == rc) {
            return (1 << lc) - 1;
        } else {
            return 1 + help(root.left, lc - 1, -1) + help(root.right, -1, rc - 1);
        }
    }
}
```
