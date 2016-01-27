[link](https://leetcode.com/problems/path-sum-ii/)

* 头节点，一定放入now

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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        if (root == null) {
            return res;
        }
        now.add(root.val);
        help(res, now, root, sum);
        return res;
    }
    private void help(List<List<Integer>> res, List<Integer> now,
                      TreeNode root, int sum) {
        if (root.left == null && root.right == null) {
            if (sum == root.val) {
                res.add(new ArrayList<Integer>(now));
                return;
            }
        }
        if (root.left != null) {
            now.add(root.left.val);
            help(res, now, root.left, sum - root.val);
            now.remove(now.size() - 1);
        }
        if (root.right != null) {
            now.add(root.right.val);
            help(res, now, root.right, sum - root.val);
            now.remove(now.size() - 1);
        }
    }
}
```
