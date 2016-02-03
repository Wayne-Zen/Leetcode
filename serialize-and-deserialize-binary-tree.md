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
    StringBuilder sb;
    public String serialize(TreeNode root) {
        sb = new StringBuilder();
        serializeHelp(root);
        sb.deleteCharAt(sb.length() - 1);
        return sb.toString();
    }
    private void serializeHelp(TreeNode root) {
        if (root == null) {
            sb.append("#,");
        } else {
            sb.append(root.val + ",");
            serializeHelp(root.left);
            serializeHelp(root.right);
        }
    }

    // Decodes your encoded data to tree.
    int index = 0;
    public TreeNode deserialize(String data) {
        String[] vals = data.split(",");
        index = 0;
        return deserializeHelp(vals);
    }
    private TreeNode deserializeHelp(String[] vals) {
        String val = vals[index++];
        if (val.equals("#")) {
            return null;
        } else {
            TreeNode node = new TreeNode(Integer.valueOf(val));
            node.left = deserializeHelp(vals);
            node.right = deserializeHelp(vals);
            return node;
        }
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

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
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
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
        sb.deleteCharAt(sb.length() - 1);
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] strs = data.split(",");
        if (strs[0].equals("#")) {
            return null;
        }
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        TreeNode root = new TreeNode(Integer.valueOf(strs[0]));
        q.offer(root);
        int index = 0;
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            index++;
            if (strs[index].equals("#")) {
                node.left = null;
            } else {
                node.left = new TreeNode(Integer.valueOf(strs[index]));
                q.offer(node.left);
            }
            index++;
            if (strs[index].equals("#")) {
                node.right = null;
            } else {
                node.right = new TreeNode(Integer.valueOf(strs[index]));
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
