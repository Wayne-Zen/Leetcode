[Link](http://www.lintcode.com/en/problem/remove-node-in-binary-search-tree/#)

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param value: Remove the node with given value.
     * @return: The root of the binary search tree after removal.
     */
    public TreeNode removeNode(TreeNode root, int value) {
        if (root == null) {
            return null;
        } else if (value > root.val) {
            root.right = removeNode(root.right, value);
        } else if (value < root.val) {
            root.left = removeNode(root.left, value);
        } else {
            if (root.left == null && root.right == null) {
                return null;
            } else if (root.left == null && root.right != null) {
                root = root.right;
            } else if (root.left != null && root.right == null) {
                root = root.left;
            } else {
                TreeNode successor = root.right;
                while (successor.left != null) {
                    successor = successor.left;
                }
                root.val = successor.val;
                root.right = removeNode(root.right, successor.val);
            }
        }
        return root;
    }
}
```
