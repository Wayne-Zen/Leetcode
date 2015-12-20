[Link](https://leetcode.com/problems/binary-tree-vertical-order-traversal/)

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
    class TreeNodeCol {
        TreeNode node;
        int col;
        public TreeNodeCol(TreeNode node, int col) {
            this.node = node;
            this.col = col;
        }
    }
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) {
            return res;
        }
        TreeMap<Integer, List<Integer>> map = new TreeMap<Integer, List<Integer>>();// col -> valset
        Queue<TreeNodeCol> q = new LinkedList<TreeNodeCol>();
        q.offer(new TreeNodeCol(root, 0));
        while (!q.isEmpty()) {
            TreeNodeCol wrap = q.poll();
            if (map.containsKey(wrap.col)) {
                map.get(wrap.col).add(wrap.node.val);
            } else {
                List<Integer> vals = new ArrayList<Integer>();
                vals.add(wrap.node.val);
                map.put(wrap.col, vals);
            }
            if (wrap.node.left != null) {
                q.offer(new TreeNodeCol(wrap.node.left, wrap.col - 1));
            }
            if (wrap.node.right != null) {
                q.offer(new TreeNodeCol(wrap.node.right, wrap.col + 1));
            }
        }
        for (List<Integer> l : map.values()) {
            res.add(l);
        }
        return res;
    }
}
```
