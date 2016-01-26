[Link](https://leetcode.com/problems/count-univalue-subtrees/)

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
    int cnt = 0;
    public int countUnivalSubtrees(TreeNode root) {
        help(root);
        return cnt;
    }
    public boolean help(TreeNode root) {
        if (root == null) {
            return true;
        }
        boolean left = help(root.left);
        boolean right = help(root.right);
        if (!left || !right) {
            return false;
        } else if (root.left != null && root.left.val != root.val) {
            return false;
        } else if (root.right != null && root.right.val != root.val) {
            return false;
        }
        cnt++;
        return true;
    }
}
```
