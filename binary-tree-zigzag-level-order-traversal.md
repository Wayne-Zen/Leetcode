[Link](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

* use stack

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) {
            return res;
        }
        boolean l2r = true;
        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);
        while (!stack.isEmpty()) {
            Stack<TreeNode> newStack = new Stack<TreeNode>();
            List<Integer> sub = new ArrayList<Integer>();
            while (!stack.isEmpty()) {
                TreeNode node = stack.pop();
                sub.add(node.val);
                if (l2r) {
                    if (node.left != null) {
                        newStack.push(node.left);
                    }
                    if (node.right != null) {
                        newStack.push(node.right);
                    }
                } else {
                    if (node.right != null) {
                        newStack.push(node.right);
                    }
                    if (node.left != null) {
                        newStack.push(node.left);
                    }
                }
            }
            l2r = !l2r;
            stack = newStack;
            res.add(sub);
        }
        return res;
    }
}
```
