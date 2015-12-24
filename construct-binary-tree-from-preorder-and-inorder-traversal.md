[Link](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

![](img/Photos/construct-binary-tree-from-preorder-and-inorder-traversal.jpg)


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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return help(preorder, inorder, 0, preorder.length - 1, 0, inorder.length - 1);
    }
    private TreeNode help(int[] preorder, int[] inorder, int lo1, int hi1, int lo2, int hi2) {
        if (lo1 > hi1) {
            return null;
        }
        int val = preorder[lo1];
        int index = 0;
        for (int i = lo2; i <= hi2; i++) {
            if (val == inorder[i]) {
                index = i;
            }
        }
        int len = index - lo2;
        TreeNode root = new TreeNode(val);
        root.left = help(preorder, inorder, lo1 + 1, lo1 + len, lo2, lo2 + len - 1);
        root.right = help(preorder, inorder, lo1 + len + 1, hi1, lo2 + len + 1, hi2);
        return root;
    }
}
```
