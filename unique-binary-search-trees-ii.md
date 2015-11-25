[Link](https://leetcode.com/problems/unique-binary-search-trees-ii/)

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
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) {
            return new ArrayList<TreeNode>();
        }
        return genTree(1, n);
    }
    private List<TreeNode> genTree(int start, int end) {
        List<TreeNode> res = new ArrayList<TreeNode>();
        if (start > end) {
            res.add(null);
            return res;
        }
        for (int k = start; k <= end; k++) {
            List<TreeNode> ltrees = genTree(start, k - 1);
            List<TreeNode> rtrees = genTree(k + 1, end);
            for (int i = 0; i < ltrees.size(); i++) {
                for (int j = 0; j < rtrees.size(); j++) {
                    TreeNode root = new TreeNode(k);
                    root.left = ltrees.get(i);
                    root.right = rtrees.get(j);
                    res.add(root);
                }
            }
        }
        return res;
    }
}
```
