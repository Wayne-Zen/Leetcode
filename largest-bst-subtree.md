[Link](https://leetcode.com/problems/largest-bst-subtree/)

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
    class ResType {
        boolean isBST;
        int upper;
        int lower;
        int size;
        public ResType(boolean isBST, int upper, int lower, int size) {
            this.isBST = isBST;
            this.upper = upper;
            this.lower = lower;
            this.size = size;
        }
    }
    int max = 0;
    public int largestBSTSubtree(TreeNode root) {
        if (root == null) {
            return 0;
        }
        help(root);
        return max;
    }
    public ResType help(TreeNode root) {
        if (root == null){
            return null;
        } 
        ResType left = help(root.left);
        ResType right = help(root.right);
        int lower = root.val;
        int upper = root.val;
        int cnt = 1;
        if (left != null) {
            if (!left.isBST || left.upper >= root.val) {
                return new ResType(false, -1, -1, -1);
            }
            cnt += left.size;
            lower = left.lower;
        }
        if (right != null) {
            if (!right.isBST || right.lower <= root.val) {
                return new ResType(false, -1, -1, -1);
            }
            cnt += right.size;
            upper = right.upper;
        }
        max = Math.max(max, cnt);
        return new ResType(true, upper, lower, cnt);
    }
}
```
