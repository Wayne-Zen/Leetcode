[Link](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return help(inorder, postorder, 0, inorder.length - 1, 0, postorder.length - 1);
    }
    private TreeNode help(int[] inorder, int[] postorder, int lo1, int hi1, int lo2, int hi2) {
        if (lo1 > hi1) {
            return null;
        }
        int val = postorder[hi2];
        int index = 0;
        for (int i = lo1; i <= hi1; i++) {
            if (inorder[i] == val) {
                index = i;
                break;
            }
        }
        int len = index - lo1;
        TreeNode root = new TreeNode(val);
        root.left = help(inorder, postorder, lo1, index - 1, lo2, lo2 + len - 1);
        root.right = help(inorder, postorder, index + 1, hi1, lo2 + len, hi2 - 1);
        return root;
    }
}
```
