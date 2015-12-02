[Link](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/)

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
    int max = 0;
    public int longestConsecutive(TreeNode root) {
        if (root == null) {
            return 0;
        }
        help(root);
        return max;
    }
    
    private int help(TreeNode root) {
        int lLen = 1;
        int rLen = 1;
        if (root.left != null) {
            int lAdd = help(root.left);
            if (root.val + 1 == root.left.val) {
                lLen += lAdd;
            }
        }
        if (root.right != null) {
            int rAdd = help(root.right);
            if (root.val + 1 == root.right.val) {
                rLen += rAdd;
            } 
        }
        int len = Math.max(lLen, rLen);
        max = Math.max(max, len);
        return len;
    }
 }
```
