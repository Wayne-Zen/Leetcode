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
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        StringBuilder sb = new StringBuilder();
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node == null) {
                sb.append("#,");
            } else {
                sb.append(node.val + ",");
                q.offer(node.left);
                q.offer(node.right);
            }
        }
        return sb.deleteCharAt(sb.length() - 1).toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] tokens = data.split(",");
        int index = -1;
        TreeNode root = tokens[++index].equals("#") ? null : 
                            (new TreeNode(Integer.valueOf(tokens[index])));
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node == null) {
                continue;
            } else {
                node.left = tokens[++index].equals("#") ? null : 
                            (new TreeNode(Integer.valueOf(tokens[index])));
                node.right = tokens[++index].equals("#") ? null : 
                            (new TreeNode(Integer.valueOf(tokens[index])));
                q.offer(node.left);
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
