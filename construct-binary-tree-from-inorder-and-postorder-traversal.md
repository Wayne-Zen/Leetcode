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
        if (inorder == null || inorder.length == 0) {
            return null;
        }
        if (postorder == null || postorder.length == 0) {
            return null;
        }
        if (inorder.length != postorder.length) {
            return null;
        }
        return help(inorder, postorder, 0, inorder.length, 0, postorder.length);
    }
    private TreeNode help(int[] inorder, int[] postorder, int is, int ie, int ps, int pe) {
        if (is >= ie || ps >= pe 
                || is < 0 || ie > inorder.length
                || ps < 0 || pe > postorder.length) {
            return null;    
        }
        TreeNode root = new TreeNode(postorder[pe - 1]);
        int mid = 0;
        for (int i = is; i < ie; i++) {
            if (inorder[i] == root.val) {
                mid = i;
            }
        }
        int L = mid - is;
        int R = ie - is - L - 1;
        root.left = help(inorder, postorder, is, is + L, ps, ps + L);
        root.right = help(inorder, postorder, is + L + 1, ie, ps + L, pe - 1);
        return root;
    }
}
```
