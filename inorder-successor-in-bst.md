[Link](https://leetcode.com/problems/inorder-successor-in-bst/)

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
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        while (root.val != p.val) {
            if (root.val < p.val) {
                root = root.right;
            } else {
                stack.push(root);
                root = root.left;
            }
        }
        if (p.right != null) {
            root = p.right;
            while (root.left != null) {
                root = root.left;
            }
            return root;
        } else {
            return stack.isEmpty() ? null : stack.pop();
        }
    }
}
```
