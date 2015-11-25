[Link](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

* 注意存储累加结果

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
    public int sumNumbers(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int[] res = new int[1];
        res[0] = 0;
        help(root, 0, res);
        return res[0];
    }
    
    private void help(TreeNode root, int sum, int[] res) {
        if (root == null) {
            return;
        }
        sum += root.val;
        if (root.left == null && root.right == null) {
            res[0] += sum;
        }
        sum *= 10;
        help(root.left, sum, res);
        help(root.right, sum, res);
    }
}
```
