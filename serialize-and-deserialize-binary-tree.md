[Link](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) {
            return "[]";
        }
        List<String> res = new ArrayList<String>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node == null) {
                res.add("null");
            } else {
                res.add(String.valueOf(node.val));
                q.offer(node.left);
                q.offer(node.right);
            }
        }
        return "[" + String.join(",", res) + "]";
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.equals("[]")) {
            return null;
        }
        String[] arr = data.substring(1, data.length() - 1).split(",");
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        int index = 0;
        TreeNode root = new TreeNode(Integer.valueOf(arr[0]));
        q.offer(root);
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            String ls = arr[++index];
            String rs = arr[++index];
            if (ls.equals("null")) {
                node.left = null;
            } else {
                node.left = new TreeNode(Integer.valueOf(ls));
                q.offer(node.left);
            }
            if (rs.equals("null")) {
                node.right = null;
            } else {
                node.right = new TreeNode(Integer.valueOf(rs));
                q.offer(node.right);
            }
        }
        return root;   
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```
