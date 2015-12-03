[Link](https://leetcode.com/problems/closest-binary-search-tree-value/)

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
    public int closestValue(TreeNode root, double target) {
        int val = 0;
        double min = Double.MAX_VALUE;
        while (root != null) {
            if (Math.abs(target - root.val) < min) {
                min = Math.abs(target - root.val);
                val = root.val;
            }
            if (root.val < target) {
                root = root.right;
            } else {
                root = root.left;
            }
        }
        return val;
    }
}
```
