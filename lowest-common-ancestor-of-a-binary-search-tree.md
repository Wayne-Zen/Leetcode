[Link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
         while ((p.val - root.val) * (q.val - root.val) > 0) {
             if (p.val > root.val) {
                 root = root.right;
             } else {
                 root = root.left;
             }
         }
        return root;
    }
}
```
