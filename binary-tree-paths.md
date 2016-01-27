[Link](https://leetcode.com/problems/binary-tree-paths/)

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<String>();
        if (root == null) {
            return res;
        }
        List<String> left = binaryTreePaths(root.left);
        List<String> right = binaryTreePaths(root.right);
        for (String s : left) {
            res.add(root.val + "->" + s);
        }
        for (String s : right) {
            res.add(root.val + "->" + s);
        }
        if (left.size() == 0 && right.size() == 0) {
            res.add(String.valueOf(root.val));
        }
        return res;
    }
}
```
