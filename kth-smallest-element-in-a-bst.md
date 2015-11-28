[Link](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

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
    public int kthSmallest(TreeNode root, int k) {
        int[] kArr = new int[]{k};
        int[] rArr = new int[]{0};
        visit(root, kArr, rArr);
        return rArr[0];
    }
    
    private void visit(TreeNode root, int[] k, int[] r) {
        if (root == null) {
            return;
        }
        visit(root.left, k, r);
        k[0] = k[0] - 1;
        if (k[0] == 0) {
            r[0] = root.val;
        }
        visit(root.right, k, r);
    }
}
```
