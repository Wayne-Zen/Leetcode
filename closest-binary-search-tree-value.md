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
        double diff = Double.MAX_VALUE;
        int res = 0;
        while (root != null) {
            double newDiff = Math.abs(root.val - target);
            if (newDiff <= diff) {
                diff = newDiff;
                res = root.val;
            } 
            if (root.val < target) {
                root = root.right;
            } else if (root.val > target){
                root = root.left;
            } else {
                break;
            }
        }
        return res;
    }
}
```
