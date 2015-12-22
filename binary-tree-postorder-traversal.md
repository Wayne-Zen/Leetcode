[Link](https://leetcode.com/problems/binary-tree-postorder-traversal/)


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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        if (root == null) {
            return res;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);
        TreeNode prev = root;
        while (!stack.isEmpty()) {
            root = stack.peek();
            if ((root.left == null && root.right == null) 
                    || prev == root.left || prev == root.right) {
                root = stack.pop();
                res.add(root.val);
                prev = root;
            } else {
                if (root.right != null) {
                    stack.push(root.right);
                }
                if (root.left != null) {
                    stack.push(root.left);
                }
            }
        }
        return res;
    }
}
```
