[Link](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) {
            return res;
        }
        LinkedList<TreeNode> q = new LinkedList<TreeNode>();
        Stack<List<Integer>> stack = new Stack<List<Integer>>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> sub = new ArrayList<Integer>();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                sub.add(node.val);
                if (node.left != null) {
                    q.offer(node.left);
                }
                if (node.right != null) {
                    q.offer(node.right);
                }
            }
            stack.push(sub);
        }
        while (!stack.isEmpty()) {
            res.add(stack.pop());
        }
        return res;
    }
}
```
