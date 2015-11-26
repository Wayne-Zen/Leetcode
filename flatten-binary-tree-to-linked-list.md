[Link](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

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
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        getTail(root);
    }
    
    private TreeNode getTail(TreeNode root) {
        if (root.left == null && root.right == null) {
            return root;
        } else if (root.left == null && root.right != null) {
            return getTail(root.right);
        } else if (root.right == null && root.left != null) {
            root.right = root.left;
            root.left = null;
            return getTail(root.right);
        } else {
            TreeNode leftTail = getTail(root.left);
            TreeNode rightTail = getTail(root.right);
            TreeNode temp = root.right;
            root.right = root.left;
            root.left = null;
            leftTail.right = temp;
            return rightTail;
        }
        
    }
}
```
