[Link](https://leetcode.com/problems/closest-binary-search-tree-value-ii/)

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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> res = new LinkedList<Integer>();
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        while (!stack.isEmpty()) {
            root = stack.pop();
            if (res.size() < k) {
                res.add(root.val);
            } else {
                if (Math.abs(root.val - target) < Math.abs(res.get(0) - target)) {
                    res.remove(0);
                    res.add(root.val);
                } else {
                    return res;
                }
            }
            root = root.right;
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
        }
        return res;
    }
}
```
