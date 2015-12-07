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
    class Wrapper {
        TreeNode node;
        int col;
        public Wrapper(TreeNode node, int col) {
            this.node = node;
            this.col = col;
        }
    }
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) {
            return res;
        }
        Queue<Wrapper> q = new LinkedList<Wrapper>();
        Wrapper rootWrapper = new Wrapper(root, 0);
        q.offer(rootWrapper);
        HashMap<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
        List<Integer> valSet = new ArrayList<Integer>();
        valSet.add(rootWrapper.node.val);
        map.put(0, valSet);
        while (!q.isEmpty()) {
            Wrapper wrapper = q.poll();
            int col = wrapper.col;
            TreeNode node = wrapper.node;
            if (node.left != null) {
                Wrapper lWrapper = new Wrapper(node.left, col - 1);
                q.offer(lWrapper);
                if (!map.containsKey(col - 1)) {
                    List<Integer> lvalSet = new ArrayList<Integer>();
                    lvalSet.add(lWrapper.node.val);
                    map.put(col - 1, lvalSet);
                } else {
                    map.get(col - 1).add(lWrapper.node.val);
                }
            }
            if (node.right != null) {
                Wrapper rWrapper = new Wrapper(node.right, col + 1);
                q.offer(rWrapper);
                if (!map.containsKey(col + 1)) {
                    List<Integer> rvalSet = new ArrayList<Integer>();
                    rvalSet.add(rWrapper.node.val);
                    map.put(col + 1, rvalSet);
                } else {
                    map.get(col + 1).add(rWrapper.node.val);
                }
            }
        }
        Set<Integer> cols = map.keySet();
        List<Integer> colList = new ArrayList<Integer>(cols);
        Collections.sort(colList);
        for (int col : colList) {
            res.add(map.get(col));
        }
        return res;
    }
}
```
