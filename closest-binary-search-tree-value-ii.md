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
        Stack<TreeNode> bigger = new Stack<TreeNode>();
        Stack<TreeNode> smaller = new Stack<TreeNode>();
        TreeNode node = root;
        // log(n)
        while (node != null) {
            if (node.val < target) {
                smaller.push(node);
                node = node.right;
            } else {
                bigger.push(node);
                node = node.left;
            }
        }
        List<Integer> res = new ArrayList<Integer>();
        while (k > 0) {
            if (bigger.isEmpty() || (!smaller.isEmpty() &&
                                (bigger.peek().val - target) > (target - smaller.peek().val))) {
                node = smaller.pop();
                res.add(node.val);
                // next smaller
                node = node.left;
                while (node != null) {
                    smaller.push(node);
                    node = node.right;
                }
            } else {
                node = bigger.pop();
                res.add(node.val);
                // next bigger
                node = node.right;
                while (node != null) {
                    bigger.push(node);
                    node = node.left;
                }
            }
            k--;
        } 
        return res;
    }
}
```
