[Link](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

    如果BST节点TreeNode的属性可以扩展，则再添加一个属性leftCnt，记录左子树的节点个数
    记当前节点为node
    当node不为空时循环：
    若k == node.leftCnt + 1：则返回node
    否则，若k > node.leftCnt + 1：则令k -= node.leftCnt + 1，令node = node.right
    否则，node = node.left

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
        int cnt = 1;
        Stack<TreeNode> stack = new Stack<TreeNode>();
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        while (!stack.isEmpty()) {
            root = stack.pop();
            if (cnt == k) {
                return root.val;
            }
            cnt++;
            root = root.right;
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
        }
        return -1;
    }
}
```


